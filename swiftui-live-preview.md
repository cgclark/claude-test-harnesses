# SwiftUI live preview from a small package

> Lets Claude see one SwiftUI/UIKit screen of a large app in Xcode's live canvas within seconds, open it by script, and check the result from a screen capture, without building or launching the app.

**Applies to:** iOS/iPadOS apps whose full build is slow or whose screens depend on engine/C code (built for the settings pages of a game port) · **Needs:** macOS, Xcode with an iOS simulator runtime, `osascript` with Accessibility permission for System Events, `screencapture` with Screen Recording permission

## Why it exists

Asked to "show the Swift preview", Claude builds and launches the whole app on a simulator, or renders an HTML mock-up of the screen. Neither is the preview: the first takes minutes per change, the second isn't the real view. Putting a `#Preview` in the app's own project means the canvas has to build the whole app first. One loop like this cost an hour of "it takes too long" before the package below was built.

## What it does

1. A small Swift package holds the screen's real source file (symlinked from the app, never copied), stand-ins for the app symbols it calls, and a separate module with only the `#Preview`.
2. AppleScript opens the package and the preview file in Xcode and sends the refresh shortcut.
3. The canvas compiles only the package and renders the screen on a preview simulator.
4. `screencapture` grabs the screen; Claude reads the PNG.
5. Pass = the canvas shows the changed screen. If it shows "Failed to build", read the preview diagnostics (step 4 of the Recipe).

## Recipe

1. **Lay out the package** (`<tools>/<screen>-preview/`):
   ```text
   Package.swift
   Sources/<Screen>Page/<Screen>View.swift      -> symlink to <app>/UI/<Screen>View.swift
   Sources/<Screen>Page/AppStandIns.swift       stand-ins for the app's globals/bridging calls
   Sources/<Screen>Page/PreviewEntry.swift      public enum <Screen>PreviewEntry { public static func makeView() -> UIView }
   Sources/<Screen>Stubs/stubs.c + include/stubs.h   C stand-ins, if the screen calls C
   Sources/<Screen>Preview/<Screen>Preview.swift     only the #Preview
   ```
   ```swift
   // swift-tools-version:5.9
   import PackageDescription
   let package = Package(
       name: "<Screen>Preview",
       platforms: [.iOS(.v17)],
       products: [.library(name: "<Screen>Preview", targets: ["<Screen>Preview"])],
       targets: [
           .target(name: "<Screen>Stubs"),
           .target(name: "<Screen>Page", dependencies: ["<Screen>Stubs"]),
           .target(name: "<Screen>Preview", dependencies: ["<Screen>Page"]),
       ]
   )
   ```
   The screen's types stay internal; `PreviewEntry.swift` is the one public entry point. Stand-ins return the defaults you want to see (for example, a setting reads as "on").
2. **The preview file:**
   ```swift
   import SwiftUI
   import <Screen>Page
   private struct Canvas: UIViewRepresentable {
       func makeUIView(context: Context) -> UIView { <Screen>PreviewEntry.makeView() }
       func updateUIView(_ v: UIView, context: Context) {}
   }
   #Preview("<Screen>", traits: .landscapeLeft) { Canvas().ignoresSafeArea() }
   ```
3. **Open and refresh by script.** Write this to a file and run `osascript <file>.applescript` (one plain command):
   ```applescript
   tell application "Xcode"
       activate
       open "<abs path>/<screen>-preview"
       open "<abs path>/<screen>-preview/Sources/<Screen>Preview/<Screen>Preview.swift"
   end tell
   delay 2
   tell application "System Events" to keystroke "p" using {option down, command down}
   ```
   ⌥⌘↩ shows the canvas if it's hidden; ⌥⌘P refreshes it.
4. **Check it:**
   ```bash
   screencapture -x /tmp/canvas.png                       # then Read the PNG
   xcrun simctl --set previews list devices | grep Booted # the canvas's own simulator set
   xcodebuild -scheme <Screen>Preview \
     -destination 'platform=iOS Simulator,name=<device>' build   # does the package compile at all?
   # "Failed to build" in the canvas: the real error is in the preview thunk diagnostics
   strings ~/Library/Developer/Xcode/DerivedData/<screen>-preview-*/Build/Intermediates.noindex/\
   <Screen>Preview.build/Debug-iphonesimulator/<Screen>Preview-t.build/Objects-normal/arm64/*.preview-thunk.dia
   ```
5. **Another screen:** symlink its file into the `Page` module, add stand-ins for whatever it calls, add a public entry, and preview it from a small file in the `Preview` module.
6. **Optional companion, a mini-app.** For screenshots across many states (languages, themes), compile only the screen file plus stubs with `swiftc`/`clang` for the simulator, ad-hoc sign it, `simctl install`, launch with `SIMCTL_CHILD_<VAR>=<value>` to pick the state, and `simctl io <udid> screenshot`. That's a test fixture, not the live preview.

## Traps

- **The canvas thunks every file of the previewed module.** A screen file with big literal tables (layouts, translations) then fails with "unable to type-check this expression in reasonable time". Keep the `#Preview` in its own module so the screen file compiles normally.
- **`xed <project> <file>` opens the file alone** in a "Files.xcfilescontainer" window that builds for macOS: "Unable to resolve module dependency: 'UIKit'". Open the package folder first, then the file.
- **A preview inside the app project builds the whole app**, and with another platform's scheme active it says "Active scheme does not build this file".
- **AppleScript can't set a Swift package's run destination** (it stays unset). The canvas picks an iOS device anyway, so don't spend time on it.
- **The canvas has no xcactivitylog.** Build errors are only in the `*.preview-thunk.dia` files; `strings` them.
- **One preview, not one per variant**, when the screen has its own light/dark or mode toggle. Duplicate previews double the build and don't match how the app shows the screen.
- **Launching the app on a simulator is not a preview**, and neither is an HTML mock-up.
- **`screencapture -x` captures the whole display.** Xcode must be frontmost and the canvas visible, or the PNG shows something else.
- **Leftover test lines in the entry file** (forcing a layout through `UserDefaults`, say) make the canvas show a state the app never starts in. Mark them and remove them after the check.
- **Simulator panel showing the wrong device.** When several simulators are attached, an embedded simulator view can keep showing the previous one and report "already attached". Detach, attach by UDID, and confirm with a screen capture.

## What it does not cover

Behaviour that needs the real app: the engine and real bindings behind the stand-ins, input from real keyboards/mice/controllers, navigation into and out of the screen, performance, and device-only layout (safe areas on hardware, external displays). Judging the design itself stays with the human.

## Loading this into Claude

> To show or check a UI screen, use the live preview package at `<tools>/<screen>-preview` (see its README): open the package and then `Sources/<Screen>Preview/<Screen>Preview.swift` in Xcode by AppleScript, press ⌥⌘P, then `screencapture -x` and Read the PNG. Never build the full app, launch it on a simulator, or make an HTML page for this. If the canvas fails, `strings` the `*.preview-thunk.dia` files in the package's DerivedData. A new screen goes in by symlink plus stand-ins plus a public entry, never by copying the file.
