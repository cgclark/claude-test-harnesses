# Siri phrasing check

> Lets Claude check an app's Siri App Shortcut phrases from the compiled build, with no device and no speech, so a phrasing regression fails before anyone has to talk to a phone.

**Applies to:** iOS apps that ship App Intents with an `AppShortcutsProvider` (spoken trigger phrases, optionally with an entity slot such as a person or item) · **Needs:** a Debug build of the app (simulator or device), Python 3, Xcode 26+; a physical iPhone only for the optional Siri smoke test

## Why it exists

By default Claude edits the phrase list, the build passes, and it asks the user to try the phrases by voice. There
is no automated way to ask Siri whether a custom phrase routes into the app. What we checked:

| Path | Result |
|---|---|
| `xcrun simctl siri` | Removed in Xcode 27 ("Unrecognized subcommand") |
| iOS Simulator | No Siri service on any simulator |
| `AppIntentsTesting` framework | Runs intents and queries entities; no phrase-to-intent routing API |
| iPhone Mirroring | No Siri in the mirror |
| `XCUIDevice.shared.siriService.activate(voiceRecognitionText:)` | Device only. On iOS 26 it reaches built-in Siri ("what time is it", "Open `<App>`" launches the app) but every App Shortcut phrase came back "I didn't get that", even with the shortcuts visibly indexed in the Shortcuts app. The same phrases worked when spoken. |

Built for a coffee-ordering app. One build changed the primary person phrase to a possessive ("make `${person}`'s
usual"). Siri read it as a Messages search and the feature stopped working on the phone. Nothing automated could
have caught it, so the lessons were turned into rules checked against the compiled phrase list.

## What it does

1. Reads the phrase templates the build actually registers: `<App>.app/Metadata.appintents/extract.actionsdata`
   (JSON written by the App Intents metadata processor), plus the trigger name from `Info.plist`
   (`CFBundleSpokenName`, else `CFBundleDisplayName`).
2. Checks configuration rules learned on the device (below), one PASS/FAIL line each.
3. Turns each template into a regex and routes a table of utterances against a made-up roster: expected intent and
   bound slot value, or no match. A slot binds only to a roster value, as an enumerable entity query does.
4. Exits 1 on any failure. In-process intent tests then cover what a routed phrase does. Real routing is a person
   speaking to a phone.

## Recipe

**1. Find the metadata in a build.** After any Debug build:

```bash
APP=$(find <DerivedData or build dir> -name '<App>.app' -path '*Debug-iphonesimulator*' | head -1)
python3 -m json.tool "$APP/Metadata.appintents/extract.actionsdata" | less
```

The keys the check uses: `autoShortcuts[].actionIdentifier` (intent type name), `autoShortcuts[].phraseTemplates[].key`
(the phrase, with `${applicationName}` and `${<parameter>}` tokens), `actions.<Intent>.parameters[].name`, and
`queries.<EntityQuery>.defaultQueryForEntity`.

**2. Write `tools/phrasing/phrasing_check.py`** with three parts. Load:

```python
data = json.load(open(f"{app}/Metadata.appintents/extract.actionsdata"))
shortcuts = [(a["actionIdentifier"], [t["key"] for t in a.get("phraseTemplates", [])])
             for a in data.get("autoShortcuts", [])]
```

Route, mirroring how a slot binds:

```python
def to_regex(tmpl, app_name, slot="${person}"):
    t = tmpl.replace("${applicationName}", "APPX").replace(slot, "SLOTX")
    pat = re.escape(t).replace("APPX", re.escape(app_name)).replace("SLOTX", "(.+?)")
    return re.compile(r"^\s*" + pat + r"\s*$", re.I), slot in tmpl

def route(utt, roster, shortcuts, app_name):
    for intent, phrases in shortcuts:
        for tmpl in phrases:
            rx, has_slot = to_regex(tmpl, app_name)
            m = rx.match(utt)
            if not m: continue
            if has_slot:
                name = next((r for r in roster if r.lower() == m.group(1).lower()), None)
                if name: return (intent, name)
                continue            # unknown value: Siri would not bind it; try the next template
            return (intent, None)
    return None
```

Then the rules and the routing table (example values are made up):

```python
primary = person_phrases[0]
check("primary slot phrase is an action form, not possessive",
      "for ${person}" in primary and "${person}'s" not in primary)
check("no domain nouns that Siri routes elsewhere", all("<noun>" not in p.lower() for p in person_phrases))
check("every phrase carries ${applicationName}", all("${applicationName}" in p for p in person_phrases))
check("a phrase without the slot exists (app asks who)", any(p.endswith("<verb phrase>") for p in person_phrases))
check("slot parameter exists and its query is the default entity query", has_param and query_is_default)

cases = [(f"{app}, <verb> for Ada", ("<SlotIntent>", "Ada")),
         (f"{app}, <verb> for Zed",  None),                 # not in the roster: must not bind
         (f"{app}, <owner phrase>",  ("<OwnerIntent>", None))]
```

**3. Run it** after every phrasing change:

```bash
python3 tools/phrasing/phrasing_check.py                # finds the latest Debug build
python3 tools/phrasing/phrasing_check.py path/to/<App>.app
```

**4. Keep the in-process intent tests next to it.** Call the intent directly with the slot filled
(`intent.<param> = <Entity>(id:)`), and test `allEntities()` and the vocabulary refresh. This covers what a routed
phrase does, not whether Siri routes it.

```bash
xcodebuild test -project <App>.xcodeproj -scheme <scheme> \
  -destination 'platform=iOS Simulator,name=<device>' -only-testing:<App>Tests
```

**5. Optional device smoke test.** A UI-test target on a physical device can confirm that Siri is reachable and that
"Open `<App>`" launches the app. Each case calls `siriService.activate(voiceRecognitionText:)`, waits, and attaches a
screenshot (the evidence) and the scraped Siri text:

```bash
xcodebuild build-for-testing -project <App>.xcodeproj -scheme <scheme> \
  -destination 'id=<device-udid>' -only-testing:<App>UITests DEVELOPMENT_TEAM=<team>
xcrun devicectl device process launch --device <device-udid> <bundle-id>   # once, so shortcuts index
xcodebuild test-without-building -project <App>.xcodeproj -scheme <scheme> \
  -destination 'id=<device-udid>' -only-testing:<App>UITests DEVELOPMENT_TEAM=<team> \
  -resultBundlePath <out>/siri.xcresult
xcrun xcresulttool export attachments --path <out>/siri.xcresult --output-path <out>/siri_att
```

Read the screenshots. Do not report App Shortcut routing from this test; see Traps.

## Traps

- **Possessive primary phrase.** "`${person}`'s `<thing>`" was taken as a Messages search. Lead with an action form
  ("`<verb>` for `${person}`"); possessives can stay as later alternatives.
- **Domain nouns get hijacked.** A phrase containing a common place or product noun routed to Maps. Use a word the
  system domains do not claim.
- **Every phrase needs `${applicationName}`.** iOS rejects app-name-free App Shortcut phrases, so a bare phrase is not
  possible; do not plan around one.
- **Orphaned enumerable query.** An `EnumerableEntityQuery` with no phrase using its slot made a device drop the
  app's whole shortcut provider. Add or remove the slot phrase and the enumerable query together. The last rule
  only confirms the parameter and its default query both exist; add a case that a slot phrase exists whenever the
  query is enumerable.
- **Stale shortcut index.** After a rename or many cabled installs the device kept old phrases. Delete the app,
  restart the phone, reinstall, launch once. Adding a roster value needs no restart if the app calls
  `updateAppShortcutParameters()` after changing it.
- **`XCUISiriService` is not a routing oracle.** It uses the legacy Siri path; custom phrases fail there even when
  they work by voice. A FAIL from it says nothing about the feature.
- **Device UI-test prerequisites.** The phone must stay unlocked (Auto-Lock Never while testing), or
  `build-for-testing` fails with "needs to be unlocked". Settings → Developer → Enable UI Automation must be on, or
  the runner times out enabling automation mode.
- **Racy handoff detection.** `XCUIApplication(bundleIdentifier:).wait(for: .runningForeground)` false-flags when the
  app was already frontmost from a previous case. Terminate it between cases and trust the screenshot. Reading the
  Siri window after a real handoff throws `kAXErrorServerNotFound`; that is the success case.
- **The check is a model, not Siri.** It encodes rules from device failures. It cannot predict a new way Apple's
  language model misroutes a phrase. When the phone shows a new failure, add a rule or a routing case for it.

## What it does not cover

Whether Siri routes a spoken phrase into the app, how Apple Intelligence interprets it, accents and mishearings, and
the Shortcuts app's indexing on a given phone. A person says each changed phrase to the phone before release. For
the app's own speech input, use [voice-bench](voice-bench.md).

## Loading this into Claude

> Siri phrasing is gated by `python3 tools/phrasing/phrasing_check.py` after a Debug build. It reads the compiled
> phrases from `<App>.app/Metadata.appintents/extract.actionsdata` and must print PASSED. When the phone shows a
> phrasing failure, add a rule or routing case for it first. Intent behaviour is covered by `-only-testing:<App>Tests`.
> No automated test can confirm Siri routing: do not report a phrase as working from the `XCUISiriService` UI test.
> Ask for a spoken check on the device, and list the phrases that changed.
