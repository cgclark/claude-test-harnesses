# In-app strategy probe

> Lets Claude test several candidate fixes from one human action it can't fake, by building the app to try each approach in turn after that event, log each outcome, and stop at the first that works.

**Applies to:** iOS apps whose source you control, where the behaviour under test only happens after a human-only event (a headphone press that reaches Siri, a real interruption, a Bluetooth reconnect, unlocking the phone) · **Needs:** a DEBUG build on the device, a log file the app writes into its container, `xcrun devicectl` with the phone paired, a person to cause the event

## Why it exists

By default each guess costs a manual test: Claude changes one thing, builds, asks the person to press the
button and say what happened, reads the answer, and guesses again. When the event is something only a
person can cause, that is one hypothesis per round trip, and the person tires before the cause is found.
Most of those guesses could have been tried in the same run, seconds apart, if the app tried them itself.
Built for Circus, to find which of several ways back to the headphones worked after Siri took the audio.

## What it does

1. Claude lists the candidate approaches, cheapest and least disruptive first.
2. The DEBUG build runs a probe after the triggering event: check the outcome as things stand (A), then
   apply approach B and check, then C, and so on.
3. Each step writes one log line: `probe <letter> <name>: <outcome> · <state>`.
4. The probe stops at the first approach that works, or logs that none did.
5. The person causes the event once; Claude pulls the log and reads which approach worked. That approach
   becomes the fix, and the probe is removed or kept behind DEBUG.

## Recipe

**1. Make the outcome machine-checkable.** The probe needs a test that reads state, not a person's
judgement: the current audio output port, a connection's state, a file's existence. If no such check
exists, write it first (for audio, see [audio route logging](audio-route-logging.md)).

**2. Write the probe**, triggered from the handler for the event, inside `#if DEBUG` or a
[launch-argument hook](launch-argument-test-hooks.md):

```swift
#if DEBUG
func probe() async {
    // Keep running through the whole probe: iOS suspends a background app partway through otherwise.
    let grant = UIApplication.shared.beginBackgroundTask(withName: "<App> probe") {}
    defer { UIApplication.shared.endBackgroundTask(grant) }

    func outcome(_ name: String) -> Bool {
        let ok = <check>()
        EventLog.write("probe \(name): \(ok ? "OK" : "no") · \(<state description>())")
        return ok
    }
    if outcome("A as is") { return }
    let steps: [(String, () async -> Void)] = [
        ("B <first approach>",  { <apply B> }),
        ("C <second approach>", { try? await Task.sleep(for: .seconds(5)); <apply C> }),
        ("D <third approach>",  { <apply D> }),
    ]
    for (name, apply) in steps {
        await apply()
        try? await Task.sleep(for: .milliseconds(1500))   // let the system settle before checking
        if outcome(name) { return }
    }
    EventLog.write("probe: none worked")
}
#endif
```

`EventLog.write` stands for the app's own timestamped file logger. Undo or reset between steps when one
approach would hide the next one's effect; log the full state on every line so a step that "worked" for
the wrong reason shows up.

**3. Hand the event to the person**, in one line: what to do, once. Add it to the
[human-only verify queue](human-verify-queue.md) if they aren't there now. Ask for nothing but doing it
and, where it matters, what they noticed.

**4. Read the result.**

```bash
xcrun devicectl device copy from --device <device> --domain-type appDataContainer \
  --domain-identifier <bundle id> --source "<app folder>/log.txt" --destination log.txt
grep "probe" log.txt
```

The first `OK` line names the approach that worked. All `no` means none of them did: add new candidates
and run the probe again from the same single event. Run it twice more before trusting an approach that
worked once.

**5. Turn it into the fix.** Put the winning approach on the normal path, keep its log line, and remove
the other steps (or leave the probe in DEBUG for the next regression).

## Traps

- **iOS suspends the app halfway.** A probe running after the app went to the background stopped partway with no further log line. Hold a background-task grant for the whole probe and end it on every exit path.
- **Steps contaminate each other.** An approach that changes state (a reset, a re-setup) can wipe what an earlier one set, or make a later one look like it worked. Log the full state on each line, and order steps from least to most disruptive.
- **Checking too early reads a false "no".** System state settles after a change. Wait a fixed time before each check, and log how long, so a slow-but-working approach isn't dropped.
- **The probe itself can be the cause.** Checking can change what it checks (starting a mic to test the output moved the output). Note in the log what the check does, and confirm the winner on the normal path without the probe.
- **One hit is not a fix.** Repeat the event on the normal path before calling it fixed.
- **Device log times are often UTC; the person is in local time.** Convert before matching the probe to when they did the event.

## What it does not cover

The event itself: the person still makes the press, the call or the unlock. It doesn't tell why an
approach works, only which one does, and it finds nothing outside the candidate list. Checks that need a
person's judgement (sound quality, comfort) can't be the probe's outcome.

## Loading this into Claude

> When a test needs a human action you can't fake, don't spend one manual test per guess. Write a DEBUG
> probe that runs after that event: check the outcome as is (A), then try each candidate approach in turn
> (B, C, …), least disruptive first, waiting for the system to settle and logging
> `probe <letter> <name>: <outcome> · <state>` after each, and stop at the first that works. Hold a
> background-task grant for the whole probe. Ask the person to cause the event once, pull the app's log
> with `xcrun devicectl device copy from`, and take the first OK line as the candidate fix; confirm it on
> the normal path before calling it done. Report times in the person's local time.
