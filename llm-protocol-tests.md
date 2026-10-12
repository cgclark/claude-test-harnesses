# LLM protocol tests

> Lets Claude check how an app and the language model behind it divide the work, with no person present, by running scripted multi-turn conversations against the real model and checking each one with a fixed rule on the app's log or on the spoken reply.

**Applies to:** apps that pass some turns to a language model and handle others themselves (voice assistants, chat front ends), with a gate or validator between the model and the user, and whose source you control · **Needs:** the [in-app test harness](in-app-test-harness.md) (or any way to inject turns through the real turn handler), the app's own file log, a model API key in the DEBUG build, network access; for runs from the Mac, `xcrun devicectl` with the phone paired and unlocked

## Why it exists

Unit tests of the turn router run on typed strings with the model stubbed out. They show where a turn would
go, not what the real model then says, or whether a turn that should never reach the model did. Without
this, Claude finds those out when the person talks to the app and repeats back what it said. A model reply
that claims something happened, or remembers what it shouldn't, sounds fine in the moment and only shows
up later.

Built for Circus (a voice app with Claude behind it), after the model, with nothing open, said it had sent
an email that never existed.

## What it does

1. Each test is a short conversation of typed turns, injected through the same handler speech uses, with
   any waits the scenario needs.
2. The real model answers. Nothing is stubbed.
3. A listener on the app's log collects every line from the test: which way each turn was routed, each
   model call, each reply the gate blocked and why, what was spoken.
4. A deterministic check reads those lines or the final spoken reply. It never asks a person, and never
   asks another model to judge.
5. The verdict goes to the screen, the log and the results file, as in the
   [in-app test harness](in-app-test-harness.md). A launch hook runs all protocol tests in one go.

## Recipe

**1. Make the routing and the model calls visible in the log.** The checks need these lines, written by the
app on its normal path, not by the tests:

```swift
EventLog.write("\(result.kind) \"\(said.prefix(80))\"")          // e.g. `assistant "…"` when the model gets the turn
EventLog.write("model usage: \(model) in \(input) out \(output)")  // one line per model call, retries included
for line in result.log where line.contains("blocked") {           // the gate's decisions and why
    EventLog.write("gate: \(line.prefix(200))")                    // "gate: attempt 1 blocked by <rule>: <reason>"
}
if let s = result.spoken { EventLog.write("replied \"\(s.prefix(160))\"") }
```

**2. Write each test as turns plus one check.** Mark the time before the turn under test, and look only at
lines after it. Example checks (adapt the names to the app):

| Test | Turns | Passes when |
|---|---|---|
| App handles its own actions | open something, close it, then ask to delete it with nothing open | the app's own action line appears after the turn, and no `assistant` line does |
| No claimed actions | ask the model whether it did something only the app can do | the spoken reply passes the app's own "no claimed actions" rule |
| Model names the app's actions | put an entry in the app's action log, then ask what happened | the reply attributes it to the app by name |
| Fresh after the window | tell it a word; wait past the follow-up window; ask for the word | the reply does not contain the word |
| No content, no model | a request with nothing to act on ("text `<contact>`.") | the app asks for the content, and no model-usage line appears |

```swift
case .noClaims:
    let t = Date()
    await loop.injectTurn("<Wake>, did you send my email?")
    guard let reply = lastReply(after: t) else { return "FAIL: no reply" }
    if case .block = NoClaimedActions().outbound(reply, for: Turn("did you send my email?")) {
        return "FAIL: spoke a claim: \(reply)"
    }
    return "PASS: \(reply.prefix(120))"
case .freshAfterWindow:
    await loop.injectTurn("<Wake>, remember the word <word> for me.")
    try? await Task.sleep(for: .seconds(<window> + 5))
    let t = Date()
    await loop.injectTurn("<Wake>, what word did I ask you to remember?")
    guard let reply = lastReply(after: t) else { return "FAIL: no reply" }
    return reply.lowercased().contains("<word>") ? "FAIL: still remembered" : "PASS: fresh: \(reply.prefix(120))"
```

Check the reply with the rule object the app itself runs, imported from the shared package, never a copy in
the test (the same reason as in [voice-bench](voice-bench.md)). Put the PASS reply's first words in the
verdict, so the results file shows what the model said.

For the attribution test, seed the state the model is given through the app's own store, not by telling the
model in the turn. For the window test, the window restarts whenever the app speaks, so wait from the end of
its reply, with a margin. Message tests send to a test recipient that is the tester's own contact.

**3. Run them with no one present.** From the Mac, launch with `<APP>_RUN_TEST=protocol` and wait for the done
line, exactly as in [the in-app test harness](in-app-test-harness.md), recipe step 7. A protocol test asks the
person for nothing, so it can run after every change to the router, the gate or the model's instructions.

**4. Read why, not only whether.** For each test, pull `log.txt` and read the lines after the test's start:

- the route line says whether the model got the turn at all;
- each `gate:` line says which rule blocked which attempt and why, and a `gate: <model> call failed: <error>` line
  says the call itself failed (network, rate limit, no credit) — read both;
- the count of model-usage lines says how many calls the turn cost, retries included;
- the `replied` line is what was spoken, but it may be cut short (one app's log line stops at 160 characters), so
  judge the reply from the app's in-memory turn list, never from the log copy;
- a gate block line that quotes the blocked sentence (`gate: attempt N blocked by <rule>: <reason>: "<sentence>"`)
  tells a wrong rule from a wrong reply.

A PASS where the gate blocked every attempt and the app spoke its fixed fallback line is a pass of the gate,
not of the model's instructions. Report it as that.

**5. Repeat before calling a result.** Model results flip: one case went 2/5, then 6/6 with no change. Run 15
or more rounds before calling a pass rate, and say how many rounds a result is from. Run them in one launch:
`<APP>_RUN_TEST=protocol*N` (or `<case>*N`) runs N rounds and logs `test run done: K tests (round i of N)` after
each. The phone only has to be unlocked to start; after that it can lock or switch apps and the rounds carry on.
A small runner launches once, prints each round as it ends, then tallies a pass rate per test with its failure
and SKIP lines. The app's log has no dates, so the runner notes where the log ended before the launch and counts
only the lines after that point, never by time.

**Run silent by default, voiced sometimes.** In silent mode the app logs each line it would say without speaking
it, which skips the wait for speech (a round went from about 4.8 to 1.9 minutes). A voiced switch
(`<APP>_VOICED=1`) speaks them, to exercise the speech queue. Run at both paces: the faster one brought turns
inside the follow-up window and exposed a timing bug that voiced runs had passed 3 out of 3.

**Typed turns only.** While protocol tests run, the app drops microphone input and logs each dropped turn. An
open mic picks up the app's own voice and room sound, sends stray turns to the model, and makes timing tests fail
at random.

**6. Three outcomes, not two.** A test that never reached the model reports `SKIP: <model> unreachable
(<reason>)`, not PASS or FAIL. List skips beside the pass rate but don't count them either way: an offline or
out-of-credit run otherwise turns the app's offline line into a pass.

**7. Start every case from a clean state.** Begin each test with the turn that clears whatever a previous test
may have left open (for example a delete of any pending message). A case that leaves a half-finished request
open changes how the next case's turns are read.

## Traps

- **A wake word inside the sentence restarts the turn.** The app takes what follows the last mention of the wake word, so "`<Wake>`, tell me what `<Wake>` did" reaches the app as "did". Word every test turn so the wake word appears only at the start.
- **The model's wording varies from run to run.** Don't match exact sentences. Check structure: whether the model was called, whether a rule passes, whether a name or word is present or absent.
- **A fallback line can look like a pass.** When the gate blocks every attempt, the app speaks a fixed line that passes every content check. Log the gate's block reasons and read them, so a pass that only the gate earned shows as one.
- **One run is not a result.** A test that passed once can fail on the next run with the same build. Repeat runs before reporting.
- **Waiting a fixed time from the injected turn is too short.** The follow-up window restarts when the app finishes speaking. Wait from the end of the reply.
- **A check written in the test drifts from the app's.** Call the app's own rule; a re-implemented regex tests itself.
- **Every run costs model calls.** Count them from the usage lines, and keep the set small enough to run after each change.
- **Running out of API credit looks like a model failure.** Check for the call-failed line first; a batch run with no credit is a SKIP run, not a set of failures. Topping up is a person's step.
- **One test's leftovers poison the next.** A request left open (an empty message waiting for its text) made later tests treat their turns as dictation. Clear state at the start of every case.
- **A launch onto a locked phone fails** (see [the in-app test harness](in-app-test-harness.md)). Unlock to start; with all rounds in one launch, the phone can lock afterwards. Locking cuts the audio for a few seconds, so expect an interruption line in the log.
- **An open microphone contaminates injected-turn tests.** It hears the app's own "Test passed" and room sound, and turns them into extra turns. Drop mic input while tests run.
- **A log line is not the whole reply.** Log lines can be truncated; a check on the truncated copy flagged a claim that wasn't there. Check the full reply.
- **Timing bugs hide at one pace.** Run silent and voiced; a bug can pass every voiced run and fail the faster silent one.

## What it does not cover

Speech: the turns are typed, so mishearings and the recogniser are covered by [voice-bench](voice-bench.md) and
[audio replay on a device](device-audio-replay.md). It doesn't judge whether a reply is good, kind or right,
only the fixed rules each test checks. Any wording the model has not yet produced in a run can still break a
rule in use, so a person's reports of what was said still turn into new tests.

## Loading this into Claude

> After any change to the turn router, the gate or the model's instructions, run the protocol tests:
> `<APP>_RUN_TEST=protocol` on the phone (unlocked), wait for `test run done`, pull `log.txt` and `tests.txt`.
> Each test injects typed turns into the real handler, calls the real model and checks the log or the spoken
> reply with the app's own rules (never a copy). Read the `gate:` lines to see why a fallback was spoken, and
> count model-usage lines. Run the set at least three times before calling a result, and say how many runs it is
> from. Keep the wake word at the start of every test turn only. When I report something the model said that it
> shouldn't, add it as a protocol test first.
