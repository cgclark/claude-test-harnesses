# Audio replay on a device

> Lets Claude test a voice feature on the real phone with no one talking: the Mac makes each test conversation as one audio file, the app plays it into its own on-device speech recogniser in place of the microphone, and the harness reads the app's log to check what the app did.

**Applies to:** iOS apps with on-device speech input (`SpeechAnalyzer` / `SpeechTranscriber`) whose source you control · **Needs:** a Mac with Xcode (`xcrun devicectl`, `xcodebuild`, `afinfo`), `say` and the [voice-bench](voice-bench.md) export, a phone connected to the Mac and unlocked, a DEBUG build signed for that phone; confirmed on iOS 27 (iOS 26 not yet), on a phone without Apple Intelligence

## Why it exists

The simulator has no speech model, so it can't transcribe at all; a simulator harness can only type turns
into the app. [voice-bench](voice-bench.md) uses the Mac's recogniser and the shared turn logic, not the
app. Neither runs the phone's own recogniser, audio session or the app's spoken replies, so by default
Claude stops there and asks the human to ride or walk around talking to the phone.

Built for Circus. Its first run on a phone found three things the Mac bench and the simulator never showed:

- **An app bug.** The app's own spoken start cue ("say <name> to start") was taken as the wake name. That
  opened the window in which no name is needed, so the next 20 seconds of anything said went to the
  assistant. Typed turns skip the cue and the bench has no cue, so only a run on the phone could hit it.
- **The phone's recogniser splits one spoken line into two sentences**, so one line can arrive as two turns.
  The Mac's recogniser returned it as one.
- **The phone writes numbers as digits** ("10") where the Mac wrote the word ("ten").

## What it does

1. The Mac renders each scenario's lines with `say`, with the scenario's pauses between lines and optional
   wind-like noise, into one audio file per scenario.
2. The file is copied into the app's data container on the phone.
3. The app is launched with DEBUG hooks: reset its own stores, then replay that file.
4. The transcription engine reads the file at real-time speed through the same conversion path as the
   microphone tap, and holds its place while the app is speaking.
5. When the file ends, the app writes one "done" log line carrying the state to check.
6. The harness pulls the app's log and compares each turn's kind and operation, and the final state, with the
   scenario. Exit code 0 when every scenario passes.

## Recipe

**1. Write each test case once, in one scenario file every harness reads.** The Mac bench, a simulator
harness that types the lines and this device harness all load the same JSON. Add a case there and every
harness runs it; there is no second list to drift.

```json
[
  {
    "name": "note: new, add, read back, stop",
    "steps": [
      { "say": "<Name>, write a note, make a list of milk and eggs.", "kind": "note", "op": "new" },
      { "say": "Also bread for Saturday.", "kind": "note", "op": "add", "after": 5 },
      { "say": "That's it.", "kind": "note", "op": "stop" }
    ],
    "noteHas": ["milk", "eggs", "bread"],
    "noteLacks": ["that's it"]
  }
]
```

`after` is the silence before a line, in seconds. `noteHas` / `noteLacks` are words the final state must or
must not contain.

**2. Give the transcription engine an optional replay input, off by default.** It reads the file in 100 ms
chunks, runs each chunk through the same converter and sinks as the mic tap, sleeps 100 ms between chunks
(real-time speed), and calls back when the file ends:

```swift
public nonisolated func setReplayFile(_ url: URL?, finished: (@Sendable () -> Void)? = nil)

// in start():
if replay.current == nil { try await requestAuthorization() }   // a replay never touches the mic
// ...
while !Task.isCancelled {
    if pause.isSet { try? await Task.sleep(for: .milliseconds(50)); continue }   // hold while the app speaks
    // read one chunk; break at end of file; convert to the analyzer format; yield to the analyzer
    try? await Task.sleep(for: .milliseconds(100))
}
if !Task.isCancelled { finished?() }
```

The engine already pauses the mic while the app speaks; the replay obeys the same pause, so a line never
lands on top of a reply and the timing stays like a real conversation. Skipping the microphone permission
request matters: a freshly installed app otherwise sits on the permission prompt and the run hangs.

**3. Add two DEBUG hooks and a done line** (see [launch-argument-test-hooks](launch-argument-test-hooks.md)):

- `<APP>_RESET` wipes the app's own stores and log before anything loads, so each scenario starts from nothing.
- `<APP>_REPLAY=<file>` plays `<data container>/<app folder>/replay/<file>` instead of the mic, then waits a
  few seconds for the last reply, stops listening, and writes the done line.

```swift
TestHooks.fired(hook, "done · \(store.notes.count) notes · open: \(open)")
// logs: <APP>_REPLAY → done · 1 notes · open: milk, eggs, bread
```

The done line is both the signal to stop waiting and the state to check. The harness reads the note count
and the open note's text from it, so it needs no second copy of the app's storage format.

**4. Make the audio on the Mac.** voice-bench writes one file per scenario (one stock voice, a 2 s lead-in,
each line padded and placed after its `after` pause, 8 s of tail so the last turn can end):

```bash
swift run -c release --package-path <package dir> voice-bench --export <audio dir> [--wind]
```

**5. Build and install a DEBUG build on the phone.**

```bash
xcrun devicectl list devices                       # the phone must be listed
xcodebuild -project <App>.xcodeproj -scheme <scheme> -destination "id=<device-id>" \
  -derivedDataPath build -allowProvisioningUpdates build
xcrun devicectl device install app --device <device-id> build/Build/Products/Debug-iphoneos/<App>.app
```

**6. Run each scenario: copy, clear the log, launch, poll, pull.**

```bash
# the audio
xcrun devicectl device copy to --device <device-id> --domain-type appDataContainer \
  --domain-identifier <bundle-id> --source <audio dir>/01.caf --destination "<app folder>/replay/01.caf"
# overwrite the app's log with an empty file BEFORE the launch (see Traps)
: > empty.txt
xcrun devicectl device copy to --device <device-id> --domain-type appDataContainer \
  --domain-identifier <bundle-id> --source empty.txt --destination "<app folder>/log.txt"
# launch with the hooks
xcrun devicectl device process launch --device <device-id> --terminate-existing \
  -e '{"<APP>_RESET":"1","<APP>_REPLAY":"01.caf"}' <bundle-id>
# every 5 s, pull the log and look for the done line
xcrun devicectl device copy from --device <device-id> --domain-type appDataContainer \
  --domain-identifier <bundle-id> --source "<app folder>/log.txt" --destination log.txt
```

Give up after about twice the file's length plus a minute (`afinfo <file>` prints its duration); replies hold
the replay, so a run takes longer than its audio. Read only the part of the log after the last reset line.

**7. Check.** Each line's first turn must have the expected kind and operation; then the final state must
contain the `noteHas` words and none of the `noteLacks` words. Write a report per run with one log per
scenario and the audio that was played, so a failure can be heard as well as read.

## Traps

- **The last run's done line gets read.** If the log isn't cleared before the launch, the harness pulls it before the new launch's reset wipes it, finds the previous scenario's done line, and every scenario "fails" with the first one's turns. Overwrite the log with an empty file before each launch. The same happens on the simulator.
- **One spoken line can come back as two turns.** Match turns to the script by words and timing, not by position: a turn made of the line's own words, closer to that line than to the next or within about 2.5 s, is that line's continuation.
- **Numbers differ by recogniser.** Compare words with numbers as digits ("ten" → "10") on both sides.
- **A locked phone can't launch the app.** Unlock it before the run; `devicectl` fails the launch otherwise.
- **Location reads "unknown"** until location access has been allowed on that phone. Allow it once by hand, or don't check location in device runs.
- **Mishearings should stay failing.** One synthetic voice gave "bread" → "bred" and "oat" → "old". Don't add recogniser hints or loosen the checks just to pass; report them separately from logic failures (as voice-bench does).
- **No permission prompt in replay mode.** If the replay path still asks for the microphone, a fresh install waits on the prompt and the run times out with no done line.

## What it does not cover

The microphone itself, headphone and Bluetooth audio routes, real wind and road noise, human voices and
accents, and starting the app with a wake phrase through Siri. Those stay with the human on the device.

## Loading this into Claude

> Voice features are checked on the phone with the audio-replay harness before asking me to test by voice:
> `<harness command> [--only <text>] [--wind]` with the phone connected and unlocked. It exports one audio
> file per scenario from `<scenario file>` (shared with voice-bench and the simulator harness), plays each
> into the app's real transcriber with `<APP>_RESET` + `<APP>_REPLAY=<file>`, and checks the app log's done
> line and turns. Clear the app log before every launch. Add new cases to the scenario file, never to one
> harness. Leave real mishearings failing. Only the mic, headphones, real wind and Siri need me.
