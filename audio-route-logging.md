# Audio route logging

> Lets Claude tell where an app's sound went (headphones, speaker, earpiece, or some other output) without hearing it, by reading a log line the app writes with its audio route and session options at every step.

**Applies to:** iOS apps that play or record audio through `AVAudioSession` (speech output, voice input, Bluetooth headphones, external mics) and whose source you control · **Needs:** the app's source, a log file the app writes into its container, `xcrun devicectl` with the phone paired, a person wearing the headphones for the cross-check

## Why it exists

Claude can't hear the phone. Without this, it changes the audio setup, builds, and asks "did you hear it
in your headphones?" The answer comes back as "no" or "it was quiet", with nothing about where the sound
went instead, so the next change is a guess. Audio routing on iOS changes underneath the app: an
interruption, a reconnect or a refused setup can move output to another port, or silently change the
session's options, and none of it shows on screen. Built for Circus, where speech after a Siri
interruption went to an output nobody was listening to.

## What it does

1. The app writes one log line at every audio step: start, interruption began, interruption ended, each
   reconnect attempt, and just before it speaks.
2. Each line carries the current route's input and output port names and types, plus the session's
   `categoryOptions` raw value.
3. The human runs the scenario and says only what they heard.
4. Claude pulls the log and reads where output was at the moment the app spoke. Pass: the output port is
   the one intended, with the options intended. The human's report is the cross-check, not the evidence.

## Recipe

**1. One describe function for the route and options.**

```swift
import AVFoundation

enum AudioRoute {
    static func describe() -> String {
        let s = AVAudioSession.sharedInstance()
        let r = s.currentRoute
        let ins = r.inputs.map { "\($0.portName) [\($0.portType.rawValue)]" }.joined(separator: ", ")
        let outs = r.outputs.map { "\($0.portName) [\($0.portType.rawValue)]" }.joined(separator: ", ")
        return "in: \(ins.isEmpty ? "none" : ins) · out: \(outs.isEmpty ? "none" : outs) · options \(s.categoryOptions.rawValue)"
    }
}
```

**2. Log it at every step**, with what the step was (`EventLog.write` stands for the app's own
timestamped file logger):

```swift
EventLog.write("start · \(AudioRoute.describe())")
EventLog.write("interrupted · \(AudioRoute.describe())")                  // interruption began
EventLog.write("interruption ended · \(AudioRoute.describe())")
EventLog.write("reconnect (attempt \(n)) · \(AudioRoute.describe())")
EventLog.write("speaking \"\(text.prefix(30))\" · \(AudioRoute.describe())")   // just before output
```

Also log route changes (`AVAudioSession.routeChangeNotification`, with the reason) and every
`setCategory` or `setActive` that throws, with its error code. Write the log to a file in the app's
container, so it survives the app being suspended and can be pulled later.

**3. Pull and read it.**

```bash
xcrun devicectl device copy from --device <device> --domain-type appDataContainer \
  --domain-identifier <bundle id> --source "<app folder>/log.txt" --destination log.txt
grep -E "speaking|interrupt|reconnect|options" log.txt
```

For each `speaking` line, the `out:` part says where the sound went. Compare it with the intended port
type (`BluetoothA2DPOutput`, `Headphones`, `Speaker`, `Receiver`, …) and the options with the ones the
app set (decode the raw value against `AVAudioSession.CategoryOptions`).

**4. Cross-check with the human.** Ask what they heard and when, nothing more. If the log says
headphones and they heard nothing, the problem is volume or the device, not the route. If they disagree
with the log, the log is missing a step: add a line there.

**5. Flag a wrong output in the app as well.** A small check that an output isn't one a person would
hear (not headphones, Bluetooth, the speaker or the earpiece) can log it and show it on screen, so the
next run catches it without waiting for the human.

## Traps

- **Options change silently.** A refused `setCategory` during a reconnect left the session's `categoryOptions` at 0, wiping Bluetooth playback; the route line alone still looked plausible until the next output went elsewhere. Log the options on every line, not only the route.
- **A port's type can lie about what it is.** A wireless mic's receiver reported itself as headphones. An output that is also the current input mic, and isn't the headphones, is likely that receiver: compare names across inputs and outputs, not only types.
- **Starting the mic can move the output.** The route at "start" isn't the route at "speaking". Log just before each output, after the mic is running.
- **The app gets suspended mid-reconnect.** A background app's retries stop without a log line. Hold a background-task grant through any multi-step reconnect, so the log shows how it ended.
- **Mirroring or a debugger changes the audio.** iPhone Mirroring blocks the phone's mic and interrupts the session; run audio tests with it closed (see [iPhone Mirroring driving](iphone-mirroring-driving.md)).
- **Device log times are often UTC; the human is in local time.** Swift's ISO 8601 stamps default to UTC. Convert before matching a line to "I heard it at …" or reporting a time.

## What it does not cover

Whether the sound was loud enough or clear, whether the headphones were actually worn, Bluetooth
pairing, and audio from other apps (Siri, music). The log proves where the app sent its audio, not that a
person heard it; the human's report covers that.

## Loading this into Claude

> Never ask "did you hear it?" as the test. The app logs `AudioRoute.describe()` (input and output port
> names and types, plus `categoryOptions`) at start, interruption began and ended, every reconnect attempt,
> every route change and just before it speaks. After an audio test, pull the app's log with
> `xcrun devicectl device copy from --domain-type appDataContainer` and read where each output went and
> with which options; pass only if it is the intended port with the intended options. Ask the human only
> what they heard, as a cross-check, and add a log line wherever the two disagree. Quit iPhone Mirroring
> before audio tests. Report times in the human's local time.
