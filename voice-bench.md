# voice-bench

> Lets Claude test a speech feature end to end on the Mac, with no one speaking: synthesized voices go through Apple's on-device transcriber and into the app's real turn logic, and every line comes back as said → heard → did.

**Applies to:** iOS/macOS apps with voice input (wake words, dictation, spoken commands) whose turn logic can live in a Swift package · **Needs:** macOS 26+ with the on-device speech model for your locale installed, Xcode / Swift 6 toolchain, `/usr/bin/say` with a few installed voices

## Why it exists

The iOS simulator has no on-device speech model: `SpeechTranscriber` reports `localeUnsupported`. So by default
Claude can unit-test the parser on typed strings, then hands the phone to the human and asks them to talk. Every
voice bug becomes a round trip through someone's mouth, and "it doesn't work" arrives with no transcript.

Built for a hands-free voice assistant, after the user reported that almost nothing in the voice path was working
or effectively tested. The first full run showed the logic was right whenever the words were heard right; the real
failure was the wake name, which the transcriber heard 9 times in 30.

## What it does

1. `say` renders each scripted line to an audio file with several Mac voices.
2. Each clip is padded with 1 s of silence each side, and optionally mixed with low-passed noise as rough wind.
3. `SpeechAnalyzer` + `SpeechTranscriber` transcribe the file on device (same model family the phone uses).
4. The transcript is fed to the **same** turn-logic type the app runs (from a shared package, never a copy),
   with a simulated clock for pauses between lines.
5. Checks per line (expected kind/operation) and per scenario (words the final result must / must not contain).
   Each failure prints said → heard → did, so it reads as a **transcription** error or a **logic** error.
   Exit code 0 when everything passes.

## Recipe

**1. Put the turn logic in a package both targets link.** The app and the bench must call the same type
(e.g. `Conversation.turn(_:at:)`). If the logic lives in the app target, move it out first. A copy in the bench
tests the copy.

**2. Check the Mac has the model.**

```swift
print(SpeechTranscriber.isAvailable, await SpeechTranscriber.installedLocales)
// if your locale is missing:
// if let req = try await AssetInventory.assetInstallationRequest(supporting: [transcriber]) { try await req.downloadAndInstall() }
```

**3. Keep the scenarios in one JSON file** that every harness reads (format in [device-audio-replay](device-audio-replay.md#recipe), step 1).

**4. Add an executable target** to the package:

```swift
.executableTarget(name: "voice-bench", dependencies: ["<SharedLogic>"]),
```

**5. Write `Sources/voice-bench/main.swift`** with these parts:

```swift
// Scenario = lines to say + expected handling + words the end state must contain / lack. Read them from the
// project's one scenario file (JSON), the same file the simulator and device harnesses read; never a list in code.
struct Step: Decodable { var say: String; var kind: <Kind>; var op: <Op>?; var after: TimeInterval? }
struct Scenario: Decodable { var name: String; var steps: [Step]; var noteHas: [String]?; var noteLacks: [String]? }
let scenarios = try JSONDecoder().decode([Scenario].self, from: Data(contentsOf: <scenario file URL>))

// Render a line. `say` can wedge: kill it after ~20 s and fail only that line.
func speak(_ text: String, voice: String, to url: URL) throws {
    let p = Process()
    p.executableURL = URL(fileURLWithPath: "/usr/bin/say")
    p.arguments = ["-v", voice, "-o", url.path, "--data-format=LEF32@22050", text]
    try p.run()
    let deadline = Date().addingTimeInterval(20)
    while p.isRunning && Date() < deadline { Thread.sleep(forTimeInterval: 0.05) }
    if p.isRunning { p.terminate(); throw NSError(domain: "say timed out", code: -1) }
}

// Pad 1 s of silence each side (and optionally add noise) with AVAudioFile/AVAudioPCMBuffer,
// writing a new file. Brown-ish noise: last = last*0.97 + rand(-1...1)*0.03; sample += last*level*12.

// Transcribe a file: finished sentences only.
func transcribe(_ url: URL) async throws -> [String] {
    let t = SpeechTranscriber(locale: Locale(identifier: "<en-US>"), transcriptionOptions: [],
                              reportingOptions: [], attributeOptions: [])
    let analyzer = SpeechAnalyzer(modules: [t])
    let file = try AVAudioFile(forReading: url)
    async let out: [String] = {
        var s: [String] = []
        for try await r in t.results where r.isFinal { s.append(String(r.text.characters)) }
        return s
    }()
    try await analyzer.analyzeSequence(from: file)
    try await analyzer.finalizeAndFinishThroughEndOfInput()
    return try await out
}
```

Then loop noise × voice × scenario: build a fresh instance of the shared logic (temp store, stubbed network and
side effects), advance a fake clock by `step.after`, pass each transcript to the real turn function, and compare.
Hand sentences to the logic the way the app's live loop does (e.g. a sentence that is a complete turn goes at once,
the rest wait for end of speech), or the bench tests a different flow than the phone runs.

**6. Run it** from the package directory:

```bash
swift run -c release voice-bench            # all scenarios × voices × clean and noisy
swift run -c release voice-bench --quick    # one voice, clean: the inner loop
swift run -c release voice-bench --names    # wake-name recognition rate
swift run -c release voice-bench --export <dir> [--wind]   # one audio file per scenario, for the phone
```

`--export` speaks each scenario with one voice, each line after its `after` pause, into one file per scenario
(`01.caf`, `02.caf`, ...). [device-audio-replay](device-audio-replay.md) plays those files into the app's own
transcriber on the phone, which covers what this bench can't.

**7. Measure a wake name before adopting it.** `--names` speaks each candidate in a few carrier phrases
("<Name>, write a note, buy milk.") across voices and noise, and counts how often the lowercased transcript
contains it. One project's numbers: a two-word product name 9/30 (heard as near-homophones), a three-syllable
word 21/30, a distinctive two-syllable common noun 30/30.

**8. Make it the gate.** When the phone shows a failure, add that exact phrase as a scenario in the shared
file, fix until it passes here, then run it on the phone with [device-audio-replay](device-audio-replay.md).

## Traps

- **Short clips come back empty.** A lone "Undo" rendered by `say` has no lead-in; the transcriber returns nothing.
  Pad 1 s of silence each side (on the phone the mic stream is continuous, so this matches reality).
- **Contextual-string hints hung the analyzer.** `AnalysisContext.contextualStrings` + `setContext` stalled
  transcription on macOS 26/27. Keep it behind a flag, off by default.
- **`say` wedges occasionally.** Run it as a `Process` with a timeout and one retry; fail the line, not the run.
- **Voices differ per Mac.** Filter your voice list by `AVSpeechSynthesisVoice.speechVoices()` names and keep one
  default (e.g. Samantha) that is always present, or the run silently shrinks.
- **Numbers come back as digits or words, depending on the recogniser** (the phone wrote "10" where the Mac wrote "ten"). Normalize both sides to digits before matching expected words.
- **Content mishearings are not logic failures.** "bread" → "bred", "oat" → "old". Count scenarios where every
  line was handled correctly but a content word was misheard separately, so the score measures your logic.
- **Testing a copy of the logic.** If the bench has its own parser, a pass means nothing. Import the shared package.
- **Using `isFinal` as the trigger in the live app.** In always-listening mode on device, `isFinal` may never
  arrive; the app needs to act on settled partials. The bench reads finals from a file, so it will not catch this.
- **Restart loops in the live app.** On device, audio route / configuration-change observers that restart the
  engine cancel every recognition task before it transcribes ("No speech detected" spam). Debounce them and guard
  task callbacks with a generation counter. Again: device-only, the bench cannot see it.

## What it does not cover

The phone's own recogniser and audio session (pausing while the app speaks, locked phone, interruptions; run
[device-audio-replay](device-audio-replay.md) for those), the microphone itself, AirPods or external mics, real wind and road noise, Siri and Shortcuts handoff, human accents and speech rates beyond the
installed voices, and any network-backed recognition. Those stay with the human on a device.

## Loading this into Claude

> Voice features are tested with voice-bench before any device test: `swift run -c release voice-bench --quick`
> from `<package dir>` (full run without `--quick`). The bench feeds on-device transcriptions of `say` audio into
> the same `<TurnLogic>` the app runs. When a phrase fails on the phone, add it as a scenario in
> `<scenario file>` (shared with the device and simulator harnesses) and make it pass first. `--export <dir>`
> writes the per-scenario audio for the device replay. Test any new wake name with `--names` before adopting
> it. Only mic/session, headphones, real wind and Siri need the device.
