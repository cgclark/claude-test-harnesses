# Bridge probes and live dashboard

> Lets Claude test a Linux Bluetooth audio bridge piece by piece (mic to voice assistant, codec decode, vendor-protocol bring-up, connection and stream state) and watch buffer, signal and link-mode plots live while the human listens, so a symptom can be tied to a timestamped event instead of a description.

**Applies to:** a Linux/BlueZ board relaying audio between a phone and a headset (A2DP media, HFP/SCO voice, an optional vendor control channel) · **Needs:** BlueZ with D-Bus access, Python 3 with `dbus-python` and GLib, `btmon` and `hcitool`, `libsbc` for the wideband decoder, systemd user services on the board, SSH from the dev machine, a browser on the same LAN

## Why it exists

By default Claude tests a bridge end to end: play music, ask "does it work?", and read logs afterwards. Every failure sounds the same to the listener ("it went quiet"), but there were at least three different faults behind it: the headset stopped rendering, the phone-side stream stalled, or the headset had gone straight to the phone and bypassed the bridge. Claude also kept adding recovery logic without knowing which fault it was recovering from.

Built for a phone-to-earbuds bridge on a single-board computer (Ranger). Each probe answers one question with a printed result, and the dashboard puts everything on one timeline while the human rides or listens. Two concrete payoffs:

- `sco_probe.py` proved in one run that voice audio reached HCI (1047 packets in 5 s, 271 non-silent) once a vendor command routed SCO to the HCI transport. Before that command, SCO connected but carried no data, because the controller sent it to its PCM pins.
- The dashboard's buffer plot showed that the "recovery" resync was what broke a stable stream. Buffer flat at about 35, one `/api/resync`, then a jump to 96 and a drain-drop sawtooth. It had been fired all night to "fix" the mutes.

## What it does

1. **Probe one path at a time.** Each tool connects, does one thing, and prints a verdict: SCO bytes over HCI or not, which bring-up packet kills audio, which side dropped first.
2. **Flip a flag, not the code.** Flag files in `/tmp` make the relay or HFP daemon dump raw payloads or change codec offers, so an A/B needs no edit.
3. **Record continuously.** A watchdog samples buffer depth, delivered bitrate and RSSI every second into a trace and writes named events (MUTE, RECOVERED, DIRECT, ON-BRIDGE) on its own.
4. **Plot it live.** The control daemon serves a dashboard that draws buffer, two-link RSSI, sniff/active band, ownership state and trigger ticks over a 5-minute window.
5. **Correlate.** The human says when they heard it, and Claude reads the trace and events at that timestamp.
6. **Mirror the board back** into the repo after any in-place edit, and use the dry-run checklist before any unpair.

## Recipe

All commands run on the board over SSH unless noted. Replace `<adapter-addr>`, `<phone-addr>`, `<headset-addr>`, `<board>`, `<ssh-target>`, `<port>`.

**Voice path probes** (need the HFP daemon running with its control socket, which is what triggers the assistant):

```bash
python3 tools/sco_probe.py <adapter-addr>             # → "SCO AUDIO REACHABLE OVER HCI" or "NO DATA — routed off-HCI"
python3 tools/sco_mic_test.py <adapter-addr> 15       # streams the ALSA mic into the SCO uplink; speak, dictation should appear on the phone
touch /tmp/dump_siri                                  # HFP daemon writes the SCO downlink to /tmp/siri_dl.raw
python3 tools/msbc_test.py                            # decodes it (60-byte eSCO packets, mSBC) → /tmp/siri_wb.wav
```

**Vendor control channel** (L2CAP PSM; edit the address constant at the top of each script first):

```bash
python3 aap_probe.py    # connects, then sends each bring-up packet with a 6 s pause and a banner; note the step where audio drops
python3 aap_watch.py    # enables gesture reporting once, prints tap events for 45 s while music plays
```

**State watch** (read-only, D-Bus): `python3 bt_watch.py` prints a timestamped line when either device's `Connected`, `MediaTransport1.State` or `MediaControl1` changes. Run it beside a probe to see which side dropped first. Edit its device table first.

**Dump and A/B flags** (relay and HFP daemon check for these files):

| Flag | Effect | Takes effect |
|---|---|---|
| `/tmp/dump_aac` | first 8 AAC payloads to `/tmp/aac_pkt_N.bin` | live |
| `/tmp/log_a2dp` | logs a per-second payload-size profile | live |
| `/tmp/dump_siri` | raw SCO downlink to `/tmp/siri_dl.raw` | next SCO connection |
| `/tmp/force_sbc`, `/tmp/force_aac` | stop offering AAC / SBC | relay restart (endpoint registration) |

**Telemetry and dashboard:**

```bash
systemctl --user start buf-watchdog         # buf_watchdog.py: 1 s trace + event log, observe-only
sudo python3 mic-router/sniff_sampler.py    # root: reads btmon, writes /tmp/link_mode.json (active/sniff/hold)
python3 mic-router/handoffd.py              # HTTP API + dashboard on :<port> (HANDOFF_PORT)
```

Open `http://<board-lan-address>:<port>/` on the LAN. Read endpoints: `GET /api/status`, `/api/events`, `/api/buftrace` (5 min of buffer depth with target and cap), `/api/linktrace` (RSSI of both links, link mode, ownership, events, triggers). `POST /api/arm|disarm|resync|resync-iphone|reconnect|cycle|restart` change the live audio path, so treat each as an action, not a probe.

**Reconnect monitor:** `tools/bridge_monitor.py <phone-addr> <headset-addr>` keeps both devices connected (a service, not a probe). Stop it before any pairing work.

**Mirror the board into the repo** (from the dev machine; the board is edited in place):

```bash
./sync-from-bridge.sh <board> <ssh-target>   # shared code → bridge/, board config → board/<board>/
git status                                   # review before committing
```

**Unpair through the checklist, always dry-run first:**

```bash
python3 graceful_unpair.py <peer-addr>             # prints target, running session holders, and the plan
python3 graceful_unpair.py <peer-addr> --execute   # stop holders → verify → DisconnectProfile → Disconnect → RemoveDevice → restart enabled
```

## Traps

- **A hard unpair bricked the earbuds.** Removing the bond and powering the radio down while a daemon still held the vendor control channel (plus HFP, AVRCP and media sessions) tore every session down with no protocol close. The earbuds then rejected re-pair, wouldn't finish a factory reset and stopped advertising. Only the vendor's support could recover them. Never `RemoveDevice` or power off a radio while anything holds a session. Use the checklist: it aborts if a session holder is still active.
- **The checklist removes the bond on one controller.** On a two-radio board a stale bond on the other controller still causes a link-key mismatch. Clear it per controller (`Adapter1.RemoveDevice` on each), not with `bluetoothctl remove`, which touches only the default controller.
- **The bridge's own reconnect services sabotage pairing.** The monitor and HFP daemon keep paging the target, which shows up as "Authentication Rejected" and endless connection tones. Stop them and kill stray discovery loops first, but keep the pairing agent running through the pair, or the bond won't persist.
- **Recovery actions can be the fault.** `/api/resync` and arm (which resyncs internally) broke a stable stream every time, and four recovery mechanisms added in different sessions were cycling the stream independently. `handoffd.py` defaults its auto-resync on (`AUTO_RESYNC=1` in code): set `AUTO_RESYNC=0` unless you are testing it. Keep telemetry observe-only, and audit what else auto-recovers before adding another.
- **Buffer depth is a hint, not truth.** Buffer at target was seen during dead silence: it tracks "the headset is accepting bytes", not "the speaker is playing". The human's ears are the ground truth. The relay also logs buffer only every ~500 packets (~11 s), so the 1 s trace repeats values.
- **Relay counters are block-buffered.** A "frozen" receive counter in the relay log meant nothing on a working relay. Trust the delivered-bitrate line and the listener.
- **Bind a debug dashboard to loopback, or put a login on it.** Its POST routes change live audio, so anyone who can reach the port can change what the rider hears. Never put it behind a public tunnel.
- **`pkill -f <name>` can kill your own SSH shell** when the shell's command line contains the name. Use the bracket form, `pkill -f '[n]ame'`.
- **`/tmp` flags vanish on reboot.** Anything that must persist (a codec force, a single-radio override) goes in a systemd drop-in with `ExecStartPre=-/usr/bin/touch /tmp/<flag>`.
- **A bluetooth restart drops the relay's media endpoints.** The phone then stops listing the bridge as an audio output. Restart the relay (or have it re-register when `org.bluez` reappears) after every `systemctl restart bluetooth`.
- **Hardcoded addresses in the probe scripts.** `aap_probe.py`, `aap_watch.py`, `bt_watch.py` and a few defaults carry device addresses as constants. Set them per device and never commit real ones to a public copy.
- **Mirror after every in-place edit.** The board isn't a git checkout. An edit not synced back is lost on the next reflash, and the repo stops matching what ran.

## What it does not cover

Whether it sounds right, which is the listener's call. Riding: wind, body blocking, a phone in a jersey pocket. Pairing and re-pairing, which stay with the human and a runbook, because a bad unpair can't be undone from software. Anything iOS decides about routing (device type, output selection), which is set on the phone.

## Loading this into Claude

> Bridge changes on `<board>` are tested with the probes in `bridge/tools/` and the live dashboard (`handoffd.py`, `:<port>`): one probe per path, with its printed verdict quoted. `buf-watchdog` and `sniff_sampler` stay running and observe-only, and every symptom the user reports is matched to the trace and event log at that timestamp before any change. Treat the POST routes as actions. Don't fire resync or arm to "recover", and keep `AUTO_RESYNC=0`. Run `sync-from-bridge.sh` after any in-place edit. Never remove a bond or power a radio down by hand: run `graceful_unpair.py <addr>` dry-run, show the user the plan, and execute only on their go.
