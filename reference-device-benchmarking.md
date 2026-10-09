# Reference-device benchmarking

> Lets Claude settle a hardware behaviour question from captures: the same accessory runs once against a known-good reference device and once against the device under test, and the two packet captures are diffed, so the evidence is what the reference actually did on the wire, not a guess.

**Applies to:** anything that talks to a closed accessory over a link you can sniff: Bluetooth bridges and
headphones, USB gadgets, network devices · **Needs:** a reference device that already works with the
accessory (usually a phone), a packet capture on each side (Apple PacketLogger + the iOS
Bluetooth logging profile, `btmon` on Linux/BlueZ, a USB or network sniffer), a few lines of Python to parse the
captures

## Why it exists

With a closed accessory, Claude by default reasons from the spec, from open-source reimplementations and from
symptoms. Each idea becomes a config change on the device under test, then a wait to see whether the symptom comes
back. Symptoms are intermittent, so every theory looks plausible for a while, and Claude reports "the fix" before it
is proven.

Built for a Linux Bluetooth bridge between a phone and wireless earbuds, which kept going silent. Weeks of theories
(an L2CAP mode, a kernel patch, ownership messages copied from an open-source client) were each "confirmed" by a
good run and then broken by the next mute. A capture of the phone talking to the same earbuds directly, parsed
byte by byte, settled several questions in an afternoon:

- The phone never sent any of the ownership or "hijack" messages the bridge sent every 20 s. The bridge's mechanism
  was absent from the reference, so it went on the suspect list instead of the fix list.
- On a voice-assistant request the phone kept the music stream flowing and used a separate link. The bridge, seen
  by the phone as a car stereo, got the stream suspended. That suspend was what destabilised playback.
- The direct path carried a different codec than the bridge, which overturned an earlier "the codec is identical"
  claim.
- Another bug only one earbud played was isolated in one step. Connected straight to the phone, both played, so the
  earbuds were fine and the bridge's re-connection was at fault.

## What it does

1. **Fix the variables.** Same accessory, same firmware, same content, same action script (play 60 s, pause 5 s,
   resume, trigger the assistant, ...).
2. **Capture the reference.** Run the script with the accessory on the known-good device and record its link.
3. **Capture the device under test** with the same script.
4. **Reduce both to comparable facts** with your own parser: the codec and bitrate actually carried, a count of each
   message opcode sent and received, stream gaps (suspend/resume timing), disconnect reasons, and the order of the
   opening handshake.
5. **Diff.** Anything the device under test does that the reference never does is a suspect. Anything the reference
   does that the device under test lacks is a candidate fix. Change one thing, capture again, diff again.

## Recipe

**1. Capture the reference (iPhone).** Install Apple's "Bluetooth logging" profile for iOS on the phone (without
it the trace has 0 packets), tether it by USB, trust the Mac, then:

```bash
PL=/Applications/Utilities/PacketLogger.app/Contents/Resources/packetlogger   # from Xcode's Additional Tools
$PL convert -u <iphone udid> -o ref.pklg                 # capture; stop with Ctrl-C after the script
$PL convert -i ref.pklg -o ref.txt -f itpsf              # decoded text, where Apple has a decoder
$PL throughput --a2dp -i ref.pklg -o ref-throughput.txt  # delivered A2DP rate over time
```

The phone's own routing decisions are plaintext in the Mac's unified log while it streams live:

```bash
timeout 120 log stream --level debug --predicate 'subsystem == "com.apple.bluetooth"' > ref-routing.log
```

**2. Capture the device under test (Linux/BlueZ):**

```bash
sudo btmon -w dut.btsnoop          # run the same script, then Ctrl-C
btmon -r dut.btsnoop > dut.txt     # decoded text
```

**3. Parse the bytes yourself.** Decoders hide vendor channels ("No Decoder Specified", no payload). A PacketLogger
file is a sequence of records `[4-byte length][4-byte sec][4-byte usec][1-byte type][payload]`, with type
`0x00` command, `0x01` event, `0x02` ACL sent, `0x03` ACL received:

```python
import struct, collections, sys
data = open(sys.argv[1], 'rb').read(); i = 0; pkts = []
while i + 4 <= len(data):
    ln = struct.unpack('>I', data[i:i+4])[0]      # try '<I' if lengths come out absurd
    e = data[i+4:i+4+ln]
    if len(e) < 9: break
    pkts.append((e[8], e[9:])); i += 4 + ln
ops = collections.Counter()
for t, p in pkts:
    if t == 0x01 and p[:1] == b'\x05' and len(p) >= 6:   # HCI Disconnection Complete
        print('disconnect handle=%04x reason=0x%02x' % (p[3] | p[4] << 8, p[5]))
    if t in (0x02, 0x03) and len(p) >= 9:
        cid = p[6] | p[7] << 8
        ops[(t, cid, p[8:13].hex())] += 1                # direction, channel, first payload bytes
for k, n in ops.most_common(40): print(n, k)
```

Point the opcode counter at the vendor channel's payload offset once you have found it (for the earbuds, a fixed
4-byte header then the opcode). Write the same reducer for the device under test's capture, so both sides print
the same table.

**4. Diff the tables** (sent opcodes and counts, codec, bitrate, gaps, disconnect reasons) and write the result
into the project notes as a native-vs-device-under-test table. Each later change cites the row it acts on.

**5. Use the reference for isolation.** When a symptom appears, move the accessory to the reference device. If
it goes away there, the accessory is fine and the fault is on your side.

## Traps

- **The reference capture drops on churn.** PacketLogger's live iOS session ended on every Bluetooth disconnect,
  re-pair or toggle ("connection has been lost", 0 packets). Start a fresh capture after each one, and don't
  include re-pairing in the script.
- **Handshakes only show in a capture that starts before connection.** One headset refused every command until a
  session was opened, and the opening sequence existed only in a trace started before the phone connected. Start
  capturing, then connect.
- **Decoder labels hide payloads. Raw bytes don't.** The GUI showed the vendor channel as undecoded with no bytes.
  The CLI-captured file, parsed by hand, had all of them.
- **Header byte order.** This project's notes and its working parser disagreed on the length field's endianness.
  Check the first record: if its length is larger than the file, switch `>I` to `<I`.
- **Debug-level logs are live only.** `log show` won't retrieve them later, and a backgrounded `log stream`
  buffers. Use `timeout N log stream` so it flushes on exit.
- **Reference evidence overrules an earlier conclusion.** "Ownership messages are needed to keep audio" had been
  "confirmed" by good runs. The reference never sent them. Reopen the conclusion; don't explain the capture away.
- **Intermittent symptoms need long holds.** Five clean minutes didn't prove a fix for a mute that came at
  irregular intervals; the hold needed was 10-20 min. Set the hold time from the symptom's worst observed interval, and say "promising, not conclusive"
  until it is met.
- **Copy the reference, not a reimplementation.** The open-source client the bridge copied was itself a
  third-party workaround. Where the open-source client and the reference disagree, follow the reference.
- **Some differences are hardware, not protocol.** The reference had antenna diversity and retransmission that a
  single USB dongle can't match. List those separately so they aren't chased as bugs.
- **Plausible dead ends.** A subsystem with a similar name (the touchscreen digitizer events, for earbud taps) is
  not on the link. Check that a candidate actually appears in a capture before spending a session on it.

## What it does not cover

Putting the accessory in ears, on a bike, in RF-noisy places. Pairing and unpairing (a hard unpair once bricked the
earbuds' pairing state, so that stays with the human and a runbook). Installing the logging profile on the phone. LE Audio isochronous traffic, which this capture
type didn't record.

## Loading this into Claude

> Hardware behaviour is settled by diffing captures against the reference, not by theory. Before changing
> `<device under test>`, capture `<accessory>` with `<reference device>` running `<action script>`
> (`packetlogger convert -u <udid>` on iOS, `sudo btmon -w` on Linux), reduce both with `tools/<reducer>.py` to
> opcode counts, codec, bitrate, gaps and disconnect reasons, and cite the differing row for every change. A fix is
> "promising" until it holds for `<worst symptom interval>`. Move the accessory to the reference to isolate any new
> symptom. Pairing changes and field tests are the user's.
