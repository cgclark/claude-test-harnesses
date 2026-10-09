# Bluetooth packet captures

> Lets Claude see what is actually on the Bluetooth link (connections, disconnect reasons, codec negotiation, L2CAP modes, SCO audio, power modes, signal) instead of inferring it from daemon logs and symptoms.

**Applies to:** Linux/BlueZ hosts (bridges, single-board computers, desktops) and the iPhone side of any accessory · **Needs:** `btmon` (BlueZ), optionally `hcidump` (the separate `bluez-hcidump` package on most distros) and `hcitool`; on a Mac, Xcode's Additional Tools for PacketLogger and Apple's "Bluetooth logging" profile installed on the iPhone

## Why it exists

Without a capture, Claude debugs Bluetooth from what the daemons print. Those logs say what a process tried, not what the link carried, so Claude keeps guessing at causes (codec, buffer, RF, the headset's firmware) and changes config to test each one. Built for a Linux bridge between a phone and wireless earbuds (Ranger). Captures settled questions that log reading had kept open for days:

- **The mute.** A 2-minute `btmon` capture, lined up against a mute, showed the bridge's own BlueZ sending L2CAP Disconnection Requests on all three A2DP channels, with no AVDTP Close, Suspend or Abort anywhere. The stream was torn down at the link layer, not closed by an application. It was first read as RF-driven. A strong-signal test (earbuds next to the dongle, RSSI near ideal) muted at the same rate, so RF was ruled out. The capture showed what happened on the wire. Why it happened was a separate question, settled by a separate test.
- **ERTM.** The earbuds rejected the bridge's proposed L2CAP ERTM mode ("unacceptable parameters", fell back to Basic), which ended a kernel-patch line of work.
- **Stem taps.** The earbuds sent standard AVRCP `PLAY` passthrough on every tap and the bridge answered `Accepted`. The taps went nowhere because the kernel had no `/dev/uinput`, not because the earbuds were silent.
- **SCO.** A wideband (transparent) SCO link established, but the controller put zero SCO packets on HCI; narrowband did reach HCI. That made it a controller routing limit, not a host bug.
- **Reference side.** PacketLogger on the iPhone showed the phone's own radio riding out 5-16% RF loss with beamforming and antenna diversity, which a single USB dongle can't match. That put occasional pops on the hardware list instead of the bug list.

## What it does

1. Start the capture **before** connecting, so the opening handshake is in it.
2. Reproduce the symptom and note the wall-clock time it happens.
3. Decode the capture to text and look at the window around that time: who sent the disconnect (TX or RX), the HCI reason code, AVDTP and L2CAP configuration, SCO data counts, Mode Change events.
4. Write down what the capture shows and what it doesn't. A cause inferred from it stays a hypothesis until a separate test confirms it.

## Recipe

**Linux (on the host under test):**

```bash
sudo btmon -w <name>.btsnoop          # binary capture; reproduce, then Ctrl-C
btmon -r <name>.btsnoop > <name>.txt  # decode to text
grep -nE 'Disconnect|Reason|AVDTP|Configure|Mode Change|SCO Data' <name>.txt
sudo btmon -i <N> -w <name>.btsnoop   # one controller only (index N of hciN), on a multi-radio host
```

```bash
hcitool -i <hciN> rssi <peer-addr>    # RSSI of an existing connection (relative value, see Traps)
hcitool -i <hciN> lq <peer-addr>      # link quality, 0-255
sudo hcidump -i <hciN> -X             # older text dump, hex payloads; btmon is preferred on BlueZ 5
```

**iPhone (reference side):** see [Reference-device benchmarking](reference-device-benchmarking.md), which has the PacketLogger CLI commands, the logging-profile requirement and a raw `.pklg` parser. This file doesn't repeat them.

**When a userspace stack owns the controller** (BTstack over libusb, for example), btmon sees nothing. Use that stack's own HCI dump (BTstack writes a `.pklg` when you enable its `hci_dump`) and parse it the same way.

## Traps

- **`sudo btmon` may not be found** because `sudo`'s `secure_path` lacks it. Use the full path (`sudo /usr/bin/btmon`).
- **btmon is a Linux tool.** Running it in the Mac terminal gives "command not found". SSH to the host first.
- **A capture shows what, not why.** The mute capture's first reading ("RF") was wrong. Test the inferred cause separately before acting on it.
- **`hcitool rssi` is not dBm.** It is a relative "golden range" value (0 is in range, negative is weaker). A "choppy below -16" threshold built on it fired false alarms. Use it for trends, not absolutes.
- **Polling RSSI floods HCI.** Two monitors calling `hcitool rssi` produced about 333 HCI commands in 2 minutes, on the link under test. Poll every few seconds, from one place.
- **Mode Change only fires on transitions.** A link that has sat in sniff for an hour shows no event. Seed the state at startup (read it once), then track events.
- **btmon's text layout varies by BlueZ version.** A parser that matches field names silently finds nothing on another version. Check a 10-second sample by eye first.
- **A clean capture doesn't clear the link.** Sniff-mode underruns showed as silence with a clean btmon and no errors. Look for what is missing (Mode Change events, gaps in media packets), not just for errors.
- **hci numbers can swap across reboots** on a host with two radios. Pick the controller by bus or BD address (`hciconfig <hciN> | grep Bus`), never a hardcoded `hci0`.
- **A libusb stack detaches the kernel driver.** After a BTstack session the `hciN` device stayed gone and bluetoothd wouldn't manage it when brought up by hand. Reboot to get the kernel driver back.

## What it does not cover

Over-the-air sniffing (captures here are host-side HCI only, so retransmissions inside the controller are invisible). LE Audio isochronous traffic. Field conditions: body blocking, a bike in traffic, crowded 2.4 GHz. Installing the iPhone logging profile, which the human does.

## Loading this into Claude

> For any Bluetooth fault on `<host>`, capture before theorising: `sudo /usr/bin/btmon -w <file>.btsnoop` started before connecting, reproduce, note the time, `btmon -r` to text, then report who sent the disconnect, the reason code, and the AVDTP/L2CAP/SCO events around it. State what the capture shows and, separately, what you infer from it. An inference is a hypothesis until a separate test confirms it. Treat `hcitool rssi` as relative and poll it sparingly. For the phone side, use the reference-device benchmarking harness.
