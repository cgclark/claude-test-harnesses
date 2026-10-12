# In-app test harness

> Lets Claude run a whole end-to-end test on a real phone, including steps only a body can do, by having the app run the test itself: it does every step it can, asks the person by voice only for the rest, watches its own log for each stage, and writes a verdict Claude reads from the Mac.

**Applies to:** iOS voice or hands-free apps whose source you control, where a flow mixes app steps with human-only steps (locking the phone, a headphone press, speaking to Siri) · **Needs:** the app's source, a DEBUG build on the phone, an in-app file logger, `xcrun devicectl` with the phone paired, earbuds for tests that speak instructions, a person only for the human-only steps

## Why it exists

Without it, a test of a flow like "lock the phone, hold the stem, say the phrase, the message goes out and the
app gets the mic back" is a list of instructions in the thread. The person does each step, then describes
what happened; Claude pulls the log and lines the person's account up against it by hand, with time zones
and missed steps in between. Each run costs several messages, and the person does the typing the app could
have done.

The harness moves the script into the app. The person's part shrinks to what needs a body, said in their
ear at the moment it is needed. Built for Circus (a voice app with Claude behind it). Its first runs caught
two spoken lines overlapping, which hung the app.

## What it does

1. The person opens Settings → Tests in a DEBUG build and taps a test, or Claude starts one from the Mac
   with a launch hook. Each row shows what the test needs from the person ("Nothing", "Lock the phone,
   then hold the stem and say `<phrase>`").
2. The test types its request into the app as if it had been heard. The typed turn goes through the same
   turn handler as speech, so everything after the recogniser is the real path.
3. When a step needs a body, the app says it through the earbuds ("Lock the phone.", "Now hold the stem
   and say `<phrase>`.") and waits for proof that it happened: the lock from
   `UIApplication.isProtectedDataAvailable`, a press from the app's own log.
4. A listener on the app's log writer collects every line written during the test. The test checks for
   each stage in order: the system assistant (Siri) took the audio, the shortcut started, the shortcut finished, the mic
   came back.
5. The test turns the first missing stage into a one-line verdict ("PASS: sent 4 s after the stem, back 2 s
   later" / "FAIL: Siri took the audio but the shortcut never ran"), speaks the result (with the reason on a
   fail), lists the line on screen and appends it to a results file.
6. Claude pulls the results file and the full log from the Mac and checks the verdict against the log.

## Recipe

**1. Let the log writer report each line to a listener.** One optional closure on the app's own logger
(the same one [audio route logging](audio-route-logging.md) and [the strategy probe](in-app-strategy-probe.md)
use), called before the line is written:

```swift
enum EventLog {
    nonisolated(unsafe) static var listener: (@Sendable (String) -> Void)?   // set only while a test runs
    static func write(_ line: String) {
        listener?(line)
        // ... append "<timestamp> <line>" to <app folder>/log.txt
    }
}
```

Create the log file with `FileProtectionType.completeUntilFirstUserAuthentication`, so lines still get
written while the phone is locked, which is when the interesting part of a locked-phone test happens.

**2. A runner with one case per test.** Each case declares what it needs from the person, which the Tests
screen shows under its name:

```swift
#if DEBUG
@MainActor @Observable final class TestRunner {
    enum Test: String, CaseIterable, Identifiable {
        case areYouThere = "Are you there"
        case sendLocked  = "Send, locked"
        var id: String { rawValue }
        var needs: String { /* "Nothing: the app answers itself." / "Lock the phone, then hold the stem and say …" */ }
    }
    private var seen: [(Date, String)] = []

    func run(_ test: Test) {
        seen = []
        EventLog.listener = { line in Task { @MainActor in TestRunner.shared.seen.append((Date(), line)) } }
        Task { finish(test, await perform(test)) }
    }
    func seenAt(_ needle: String, after: Date = .distantPast) -> Date? {
        seen.first { $0.0 >= after && $0.1.contains(needle) }?.0
    }
}
#endif
```

Put the Tests row in Settings inside `#if DEBUG`, and the runner too. Nothing of it reaches a release build.

**3. Inject turns through the real handler.** Add one entry point that hands text to the same function the
recogniser's finished sentence goes to, after the app has stopped speaking (see Traps):

```swift
func injectTurn(_ text: String) async {
    guard state != .idle else { return }
    for _ in 0..<60 where state == .speaking { try? await Task.sleep(for: .milliseconds(250)) }
    finals = [text]; heard = text
    await endTurn(listening: true)          // the same function speech ends in
}
```

This differs from a typed-turns launch hook ([launch-argument hooks](launch-argument-test-hooks.md)) in that
the app is already listening and stays listening, so the turn lands in a live session with its audio state.

**4. Ask for the body step, then wait on state, not on time.**

```swift
await announce("Lock the phone.")                       // spoken through the earbuds, mic paused
guard await waitUntil(seconds: 90, { !UIApplication.shared.isProtectedDataAvailable }) else {
    return "FAIL: the phone wasn't locked within 90 seconds"
}
let start = Date()
await announce("Now hold the stem and say <phrase>.")
_ = await waitUntil(seconds: 60) { seenAt("<mic back line>", after: seenAt("<shortcut finished line>")) != nil }
```

Give every wait a timeout that ends in a FAIL naming what didn't happen.

**5. Turn stages into a verdict.** Look for each stage's log line after the step's start time, and report the
first one missing. The stage lines are ones the app already writes: an interruption (the assistant took the
audio), a log line from each App Intent's `perform()` (as in [the Siri phrasing check](siri-phrasing-check.md),
step 6), and the line written when listening restarts.
`secs(a, b)` is a small helper that formats the gap between two stage times.

```swift
let took = seenAt("interrupted", after: start)
let ran  = seenAt("shortcut: <first intent> → ok", after: start)
let sent = seenAt("shortcut: <last intent>", after: start)
let back = seenAt("listening (attempt", after: sent ?? .distantFuture)
if took == nil { return "FAIL: Siri never took the audio (no stem press heard)" }
if ran  == nil { return "FAIL: Siri took the audio but the shortcut never ran" }
if sent == nil { return "FAIL: the shortcut ran but stopped before the end" }
if back == nil { return "FAIL: sent, but the app didn't get the mic back within a minute" }
return "PASS: sent \(secs(took, sent)) after the stem, back \(secs(sent, back)) later"
```

**6. Report three ways.** In `finish`: clear the listener, put the line at the top of the on-screen results,
write it to the log as `test result: …`, append it to `<app folder>/tests.txt`, and speak it through the
earbuds ("Test passed." or "Test failed." plus the reason), so the person never has to look at the phone.

**7. A launch hook for runs with no one present.** `<APP>_RUN_TEST=<name>|protocol` starts listening and runs
the named test case (the enum case name, not its on-screen title), or every protocol test
([LLM protocol tests](llm-protocol-tests.md)). Run tests one after another, a couple of seconds apart, and end
with a done line, `test run done: <n> tests`. Read the hook through the app's single hook helper, inside
`#if DEBUG`, as in [launch-argument hooks](launch-argument-test-hooks.md).

```bash
# clear the old log and results first (see the stale-log trap in launch-argument-test-hooks.md)
: > empty.txt
for f in log.txt tests.txt; do
  xcrun devicectl device copy to --device <device-id> --domain-type appDataContainer \
    --domain-identifier <bundle-id> --source empty.txt --destination "Library/Application Support/<app folder>/$f"
done
# the phone must be unlocked for this launch (see Traps)
xcrun devicectl device process launch --device <device-id> --terminate-existing \
  -e '{"<APP>_RUN_TEST":"protocol"}' <bundle-id>
# poll every few seconds for the done line, then pull the results
xcrun devicectl device copy from --device <device-id> --domain-type appDataContainer \
  --domain-identifier <bundle-id> --source "Library/Application Support/<app folder>/log.txt" --destination log.txt
grep -q "test run done" log.txt && xcrun devicectl device copy from --device <device-id> \
  --domain-type appDataContainer --domain-identifier <bundle-id> \
  --source "Library/Application Support/<app folder>/tests.txt" --destination tests.txt
```

**8. Check that a verdict is real.** A results line alone is not the evidence:

- The log has the hook's fired line (`hook <APP>_RUN_TEST → <n> tests`) from this launch, and the `test result:`
  line matches the one in `tests.txt`.
- Each stage a PASS names has its own line in `log.txt`, in order, with times that give the seconds in the
  verdict. A PASS with no stage lines around it is a test that checked the wrong thing.
- For a FAIL, the last stage line present is where it stopped; read the lines after it (the route lines from
  [audio route logging](audio-route-logging.md), errors) for why.
- Device log stamps are often UTC; convert to the person's local time before matching them to what they did.

Run a test that needs a body three times before calling it fixed, as with [the strategy probe](in-app-strategy-probe.md).

## Traps

- **A launch from the Mac fails while the phone is locked.** `devicectl` returns "device was not, or could not be, unlocked". Unlock the phone, launch, and let the test ask for the lock itself.
- **Two lines spoken at once hung the app.** A turn injected while the app was still speaking overlapped two spoken lines, and the first never reported finishing. Inject only after the app has finished speaking (wait while its state is "speaking"), and queue speech one line at a time.
- **With no earbuds, the app hears itself.** Its own voice from the loudspeaker reached the mic and was taken as a turn. Run spoken tests with earbuds connected; with the loudspeaker, a pause while speaking is not enough.
- **Stage lines from before the test count as this test's.** Match lines only after the step's start time, and clear the collected lines at the start of each test.
- **A wait without a timeout never reports.** If the person never presses, the test must still end in a FAIL that says which step it was waiting for.
- **The listener stays set after a test.** Clear it in `finish` on every path, or the next test sees lines from the last one.

## What it does not cover

The body steps themselves: someone still locks the phone, presses the stem and says the phrase. It doesn't
check what the person heard or whether Siri understood them for a reason the log can't show, and it tests
only what the app logs. Field conditions (wind, riding, other people) and release builds stay with the
person; queue those checks in [the human-only verify queue](human-verify-queue.md).

## Loading this into Claude

> End-to-end tests on the phone run in the app's DEBUG Tests screen (Settings → Tests), not as step lists in
> the thread. Each test types its request through the real turn handler, asks me by voice only for what needs a
> body, waits on state (the lock via `isProtectedDataAvailable`, stage lines via the log listener), and writes a
> one-line verdict to the screen, the log and `<app folder>/tests.txt`. From the Mac, with the phone unlocked,
> clear `log.txt` and `tests.txt`, launch with `<APP>_RUN_TEST=<name>|protocol`, wait for `test run done`, then
> pull both files. Trust a verdict only when its stage lines are in `log.txt` from this launch. Inject turns only
> after the app finishes speaking, and use earbuds for spoken tests. Add a new test case rather than asking me
> to run steps by hand.
