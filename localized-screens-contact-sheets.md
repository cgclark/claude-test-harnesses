# Localized screens and contact sheets

> Lets Claude see every key screen in every language the app ships, plus a doubled-length pseudo-locale, side by side on one page per screen, so it can find clipped, overflowing, untranslated or wrongly mirrored text itself.

**Applies to:** iOS / iPadOS apps with string catalogs or `.strings` files · **Needs:** Xcode with an iOS runtime, an XCUITest target, accessibility identifiers on the controls the walk taps, the project's own named simulator, Python 3

## Why it exists

By default Claude checks localization by reading the string catalog. That shows a translation exists, not
that it fits. Any screenshot it takes is in English, on one screen. The human then finds the German button
that wraps, the Thai title that clips, the sentence still in English because it was built with `+`, and
sends them back one at a time.

Built for Throwdown (26 languages plus English, including two right-to-left languages). One run gives a page
per screen with a column per language, which Claude reads as images.

## What it does

1. A UI test walks a fixed path through the app's key screens and takes a screenshot at each stop. Each is
   kept as an attachment named `<lang>-<n>-<screen>`.
2. It relaunches once per language with `-AppleLanguages (<code>) -AppleLocale <code>`, and once as
   `pseudo`: English with `-NSDoubleLocalizedStrings YES`, which doubles every localized string to stand in
   for a long language.
3. A script runs the test, exports the attachments from the `.xcresult`, and writes one HTML contact sheet per
   screen.
4. Claude reads the sheets (or the PNGs). Fail = text that clips, wraps badly, overlaps, stays in English in a
   translated column, or doesn't mirror in a right-to-left language.

## Recipe

**1. Identify the controls the walk needs.** Add `.accessibilityIdentifier("home.settings")` and so on. The
test taps by identifier, never by label (labels change per language) or by coordinate.

**2. The UI test** (one test method, one walk per language):

```swift
final class LocalizedScreens: XCTestCase {
    /// A step whose element never appeared: the screenshot would be of the wrong screen, so the run stops.
    struct Missing: Error, CustomStringConvertible {
        let id: String, lang: String
        var description: String { "no element \"\(id)\" in \(lang) — renamed accessibility identifier?" }
    }
    // No list here: the script reads the languages from the built app and passes them in.
    private var langs: [String] {
        (ProcessInfo.processInfo.environment["SCREENSHOT_LANGS"] ?? "").split(separator: ",").map(String.init)
    }
    func testEveryScreenInEveryLanguage() throws {
        guard !langs.isEmpty else { return XCTFail("SCREENSHOT_LANGS is empty — run tools/screenshots.sh") }
        for lang in langs { try walk(lang) }
    }

    private func walk(_ lang: String) throws {
        let app = XCUIApplication()
        let code = lang == "pseudo" ? "en" : lang
        app.launchArguments = ["-AppleLanguages", "(\(code))",
                               "-AppleLocale", code.replacingOccurrences(of: "-", with: "_"),
                               "-<inAppLanguageKey>", "system"]       // if the app has its own language picker
        if lang == "pseudo" { app.launchArguments += ["-NSDoubleLocalizedStrings", "YES"] }
        app.launch()
        defer { app.terminate() }
        snap(app, lang, "1-home")
        try tap(app, lang, "home.settings"); snap(app, lang, "2-settings")
        app.swipeUp();                       snap(app, lang, "3-settings-more")
        try tap(app, lang, "BackButton")     // iOS's own back button, for a pushed screen
        // … every key screen, then back out …
    }
    private func tap(_ app: XCUIApplication, _ lang: String, _ id: String) throws {
        let element = app.descendants(matching: .any)[id].firstMatch
        guard element.waitForExistence(timeout: 6) else {
            snap(app, lang, "0-missing-\(id)")          // what was on screen instead
            throw Missing(id: id, lang: lang)
        }
        element.tap()
    }
    private func snap(_ app: XCUIApplication, _ lang: String, _ screen: String) {
        let shot = XCTAttachment(screenshot: app.screenshot())
        shot.name = "\(lang)-\(screen)"; shot.lifetime = .keepAlways; add(shot)
    }
}
```

Dismiss the system permission alerts at the start of each walk through
`XCUIApplication(bundleIdentifier: "com.apple.springboard")`. Give the test its own scheme
(`Screenshots`) so a normal test run doesn't take a screenshot of every screen in every language.

**3. Run it and build the sheets.** Build first, then take the languages from the built app's own `.lproj`
folders. That way there is one list, used by both the test and the sheet, and nobody types it out. A
`TEST_RUNNER_` prefix passes a variable from `xcodebuild` to the test process:

```bash
xcodebuild build-for-testing -project <App>.xcodeproj -scheme Screenshots -destination "id=$UDID" -derivedDataPath build/dd
LANGS="${1:-}"
if [ -z "$LANGS" ]; then   # English, pseudo, then the rest; Base and any play languages (x-*) left out
  REST=$(cd build/dd/Build/Products/Debug-iphonesimulator/<App>.app && ls -d *.lproj | sed 's/\.lproj$//' \
         | grep -v -x -e Base -e en -e 'x-.*' | paste -sd, -)
  LANGS="en,pseudo,$REST"
fi
TEST_RUNNER_SCREENSHOT_LANGS="$LANGS" xcodebuild test-without-building -project <App>.xcodeproj -scheme Screenshots \
  -destination "id=$UDID" -derivedDataPath build/dd -resultBundlePath build/screenshots/run.xcresult
xcrun xcresulttool export attachments --path build/screenshots/run.xcresult \
  --output-path build/screenshots/raw
```

`raw/manifest.json` lists each attachment's `suggestedHumanReadableName` (your name plus a suffix) and its
`exportedFileName`. Group by screen and write one HTML page per screen: one `<figure>` per language, in the
order of `$LANGS`, with any language not in it added at the end, never dropped. Fail if a requested language
has no screenshots. Split the name at the first part that starts with a digit, because codes like `pt-BR` and
`zh-Hans` contain a dash.

**4. Read the sheets.** Check `pseudo` first: anything that survives doubled English usually survives German
and Finnish. Then check each right-to-left column for mirroring, and every column for leftover English.

```bash
tools/screenshots.sh              # every language
tools/screenshots.sh en,de,ar     # a subset while fixing
```

## Traps

- **A hand-typed language list drifts.** The test's default list and the sheet's column order were both typed
  out. The app grew to 26 languages, but the test still covered 19, so the other seven never got screenshots,
  including both right-to-left languages. The sheet also dropped any language missing from its order list.
  Fixed by step 3: one list, read from the built app's `.lproj` folders.
- **A tap that skips a missing element hides a broken walk.** The first walk tapped only if the element
  appeared. When two screens moved to iOS's own back button, their custom back identifiers disappeared, and
  for weeks the walk photographed the wrong screens without failing. `tap` now throws with the identifier and
  language, and saves a screenshot of what was there. The system back button's identifier is `BackButton`.
- **Never run it on a simulator that's running unit tests.** It kills the other test host.
- **Saved in-app language beats the launch language.** If the app has its own language picker, the saved
  choice on the simulator overrides `-AppleLanguages`. Pass the picker's key as a launch argument
  (`-<key> system`); a `-key value` argument overrides UserDefaults for that launch only and writes nothing.
  Unit tests on the same simulator read that saved choice too.
- **Some strings escape the catalog.** `Text("a" + "b")` and string-producing `.formatted()` calls didn't
  follow the in-app language; keyed `String(localized: "key", defaultValue:)` isn't extracted. The sheet shows
  them as English in translated columns. A string-check script that fails on those forms stops them coming back.
- **Arabic large titles are taller.** The navigation bar gives a large title containing Arabic letters a taller
  line (46.3 pt against 42.7 pt) and keeps the tallest it has laid out. A Latin-only title such as a brand name
  is shorter, so the first push from it opened collapsed, and so did the pop back. Hebrew, Devanagari and Thai
  measured the same as Latin. The fix is one shared large-title modifier that adds the invisible Arabic letter
  mark (U+061C) to a title with no Arabic letters when the app's language is in Arabic script. Found with
  `uikit-layout-probe.md`.
- **Right-to-left needs more than the language.** Direction was set on the root view and on every window;
  sheets don't inherit the root's. Images, custom `Shape`/`Path` drawing and UIKit gesture translations don't
  mirror by themselves. `-NSForceRightToLeftWritingDirection YES` checks layout direction in any language.
- **Don't hard-code the simulator's UDID in the script.** Resolve it by name (see `headless-ios.md`).
- **Editing the simulator's preferences doesn't reach a running app.** Change settings through launch
  arguments or the app's UI.
- **Fixed sleeps between taps** (about a second each) make a full run take minutes per language. Run a subset
  while fixing, and the full set before a release.

## What it does not cover

Whether a translation is right, or natural, is a language review. It isn't a screenshot check. Dynamic Type
sizes, other device sizes and dark/light variants aren't in this walk (add a launch argument and a column to
cover one). Screens behind live data, permissions or hardware need seeded state from
`launch-argument-test-hooks.md`. How text reads on a real phone in the hand stays with a person.

## Loading this into Claude

> Localization is checked from contact sheets, not the catalog. After a UI or string change, run
> `tools/screenshots.sh <changed langs>,pseudo` on `<App> <device>` (never while unit tests are running), then
> read `build/screenshots/<screen>.html`. The languages come from the built app; never type a list. A run that
> stops on `no element "<id>"` means the walk needs updating, not a retry. `pseudo` is doubled English and must fit everywhere. Fail on clipped
> or wrapped text, English left in a translated column, or a right-to-left column that doesn't mirror. New
> screens get an accessibility identifier and a step in `LocalizedScreens`. Run the full language set before a release.
