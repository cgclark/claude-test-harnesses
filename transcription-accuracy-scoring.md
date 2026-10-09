# Transcription accuracy scoring

> Lets Claude put a number on a speech-to-text change by running real recorded speech with a known transcript through the app and scoring the output by character error rate, instead of reading a transcript and calling it "looks right".

**Applies to:** apps or services that transcribe speech (on-device or not), especially in several languages or with
more than one engine · **Needs:** network access to a public dataset API for fetching samples, a decoder to 16 kHz
mono PCM (AVFoundation here), the app's real transcription path callable on a file or stream, and a device or Mac
that has the speech model (the iOS simulator does not)

## Why it exists

By default Claude tests a transcription change by recording a sentence, or by asking the user to talk, and then
judging the transcript by eye. That gives no number to compare between engines, languages or builds, and every
check needs a person speaking in that language.

Built for a privacy-first transcription app with several engines (Apple's on-device transcriber plus two
open-source models) across Korean, Japanese, English and Chinese. "Does the Korean transcript look right?" is not
a test. Public evaluation sets come with human transcripts, so each run can be scored.

## What it does

1. Picks a corpus for the selected language and engine: one row at a random offset, several rows stitched to a
   target length, or utterances from different speakers interleaved into a conversation.
2. Fetches rows from the public dataset API: an audio URL and the reference transcript.
3. Decodes and writes 16 kHz mono WAV, then sends it through **the same transcription path a user's file or live
   recording takes**.
4. Scores the transcript against the reference: Levenshtein distance over characters divided by reference length,
   after stripping whitespace and punctuation. Shown as `100 × (1 − CER)`, clamped to 0–100, and stored with the
   saved record.

## Recipe

**1. Choose sets that publish ground truth for your languages.** We used the evaluation sets of a published
edge-ASR paper where they were publicly reachable: Common Voice, FLEURS, Zeroth-Korean, LibriSpeech, plus
substitutes where a set was gated or unreachable (a Japanese read-speech set, MINDS-14 for Chinese). Check each
set's licence before using or redistributing its audio or text.

**2. Describe each corpus as data**, because field names differ per set:

```swift
struct TestCorpus {
    let id, name, language: String          // language = ISO 639-1 code of the speech
    let dataset, config, split: String      // e.g. "<org>/<dataset>", "<lang config>", "test"
    let rows: Int                           // split size, for random offsets
    let textKey: String                     // "sentence" | "transcription" | "text"
    let speakerKey: String?                 // "client_id" | "speaker_id" | nil = no conversation test
    let multilingual: Bool                  // the dataset spans languages (worth offering under auto-detect)
}
```

**3. Fetch rows.** The Hugging Face datasets-server returns JSON rows with signed audio URLs:

```bash
curl -s "https://datasets-server.huggingface.co/rows?dataset=<org>/<dataset>&config=<config>&split=test&offset=0&length=1" \
  | python3 -c "import json,sys; r=json.load(sys.stdin)['rows'][0]['row']; print(list(r))"
```

`row.audio` is a list of `{src, type}` (sometimes a single object); `row[textKey]` is the reference.

**4. Build the sample.** Single: one random offset. Stitched: fetch a batch, decode each clip, join with 0.3 s of
silence until the target duration, and join the references with spaces. Conversation: pull rows from as many
separate regions of the split as voices wanted (some sets are grouped by speaker), group by `speakerKey`, keep the
largest groups, and interleave round-robin.

**5. Score with CER:**

```swift
static func percent(reference: String, hypothesis: String) -> Int? {
    let drop = CharacterSet.whitespacesAndNewlines.union(.punctuationCharacters)
    func norm(_ s: String) -> [Character] {
        Array(String(String.UnicodeScalarView(s.unicodeScalars.filter { !drop.contains($0) })))
    }
    let r = norm(reference), h = norm(hypothesis)
    guard !r.isEmpty else { return nil }
    let cer = Double(levenshtein(r, h)) / Double(r.count)    // two-row DP over Characters
    return max(0, min(100, Int((1 - cer) * 100 + 0.5)))
}
```

Show the reference above the live transcript and the score once text exists (we used ≥ 90 green, ≥ 70 amber, else
red), and save the score with the record so runs can be compared later.

**6. Filter what is offered.** Offer only corpora in the selected language, never a fallback to all of them. Under
auto-detect, offer only multilingual sets. Narrow again to what the selected engine can run: a single-language model
gets its own language only; Apple's transcriber gets only locales with installed assets.

**7. Run it** on a device or a Mac with the speech model, from the app's test screen: pick dataset, speaker count
and duration, start, and read the score. Repeat the same choice on two engines or two builds to compare.

## Traps

- **WER on languages without reliable spaces.** Korean word boundaries are ambiguous (the same name spaced or
  unspaced), so word error rate would count spacing as errors. CER after stripping whitespace and punctuation
  measures the characters. For English this also
  ignores word boundaries; add WER if that matters.
- **Bare language codes.** The language detector returns `en`; the transcriber supports `en-US`. Restarting on a bare
  code threw `localeUnsupported` and wiped the live text. Map a language to a supported regional locale, and compare
  language codes, not full identifiers.
- **Falling back to every corpus.** Showing all corpora when a language had none put Japanese clips under Korean.
  Filter strictly and show a "no corpus for this language" message.
- **Single-language sets under auto-detect.** They test transcription, not language detection. Mixed-language
  audio needs its own option, not a reused flag.
- **Config count is not language count.** LibriSpeech has three configs; they are audio-quality splits.
- **Short stitched clips.** A fixed rows-per-voice count capped a 2-speaker clip near 96 s, so a 180 s request
  silently came back short. Scale the rows with the target length and leave slack for failed downloads.
- **Speaker counts beyond the diarizer.** The data had 10–44 speakers; the limit was what the diarizer could
  separate. Cap the speaker picker at the smaller of the corpus and the engine.
- **Losing the score.** It lived on the capture screen and vanished on save. Persist it with the record.
- **Testing on the simulator.** The iOS simulator has no on-device speech model; runs there fail before transcribing.
  See [voice-bench](voice-bench.md) for running Apple's transcriber on the Mac.

## What it does not cover

Live microphone capture, room noise, phone calls and accents outside the sets, and whether the transcript is useful
to the person reading it. It also does not test language detection on code-switched speech. In our project the run
is started from the app's test screen; there is no headless runner or unit test for the scorer yet.

## Loading this into Claude

> Transcription changes are scored, not eyeballed: run a corpus sample from the app's test screen on a device (or a
> Mac with the model) and report the % match (100 × (1 − CER), whitespace and punctuation stripped) per engine and
> language, before and after. Corpora are defined in `<TestCorpus.swift>`; the scorer is `<TranscriptFidelity>`.
> Offer only corpora in the selected language and only what the selected engine can transcribe. Check each dataset's
> licence before adding it.
