# Browser driving

> Lets Claude load the web page it just changed, measure it, and check it in a real browser, rather than declaring a deploy done from the source diff.

**Applies to:** websites, CMS themes, web portals, local HTML pages and artifacts (built for a WordPress theme and some web portals) · **Needs:** Claude in Chrome (browser extension, `mcp__claude-in-chrome__*` tools) for logged-in sites; the Claude desktop app's built-in browser pane (`mcp__Claude_Browser__*`) for dev servers and local pages

This harness came from Claude's own tooling, not something we built. These notes cover what we learned using it.

## Why it exists

Without a browser, Claude edits CSS or a template, deploys it, and reports success. It hasn't seen the page. On the WordPress site that missed things like these: a stylesheet served with a 403 after upload (wrong file mode), so the whole site was unstyled; a favicon change that never showed because the CMS injects its own icon links after the theme's; a layout that was right in Chrome and wrong in Safari at the same width. With a browser, Claude can read the rendered page, measure computed styles at set widths, and compare before and after.

## What it does

1. Open the page: the live or staging site in the user's Chrome (with their sign-ins), or a dev server or local file in the built-in pane.
2. Read it as text or as an accessibility tree, not from screenshots, wherever text is enough.
3. Measure what matters with the JavaScript tool: computed styles, element boxes, overflow, at fixed viewport widths.
4. Compare with a baseline taken before the change. Pass = values match the baseline, except where the change was meant to differ.
5. Screenshot only for what has to be seen, in the theme the user will actually view.

## Recipe

1. **Pick the surface.**
   - **Claude in Chrome**: the user's real Chrome profile, already logged in to admin panels and portals. Use it for anything behind a login, and whenever the user asks for Chrome. Don't offer a substitute.
   - **Built-in browser pane**: dev servers (`preview_start` with a `.claude/launch.json` entry, or with a `url`), local HTML pages, and published artifacts. It has its own sign-ins, separate from Chrome's.
2. **Bootstrap Chrome.** Load the tools in one `ToolSearch` call. Run `list_connected_browsers`. An empty result means the extension's side panel is closed, signed out, or in a different Chrome profile than the one with the extension. Ask the user which, in one line, before anything else. Open a new tab for the work rather than using the user's tabs.
3. **Read before you look.**
   ```text
   get_page_text            → visible text (copy, headings, error messages)
   read_page / find         → structure and element refs
   read_console_messages    → JS errors after a deploy
   read_network_requests    → status codes for CSS, JS and images
   ```
4. **Measure, don't eyeball.** Run a probe through the JavaScript tool at each breakpoint you care about (we used 1440, 900 and 500 px):
   ```js
   [...document.querySelectorAll('<selector>')].map(e => {
     const r = e.getBoundingClientRect(), cs = getComputedStyle(e);
     return { w: r.width, h: r.height, pad: cs.padding, font: cs.fontSize, over: e.scrollWidth > e.clientWidth };
   })
   ```
   Save the output before the change, then diff it afterwards. We reconciled a theme's source and build stylesheets this way. The probes at three widths matched the pre-deploy baseline exactly before we called it done. For text-wrapping decisions, measure in the DOM (set the candidate text, read its width) before saving anything.
5. **Check dark mode deliberately in the pane.** The built-in pane renders local pages and static previews in light mode. Before a screenshot of a themed page, force dark:
   ```js
   document.documentElement.dataset.theme = 'dark'
   ```
   Check light mode only when the change is colour-specific. Otherwise the dark colours are never checked, and the user sees a light preview that doesn't match what they view.
6. **Confirm the deploy from outside the browser too.** `curl -sI <asset url>` should return 200 for each deployed file, and `curl -s <page> | grep '<expected tag>'` shows what the server actually sends, without any browser cache.

## Traps

- **Site approvals in Chrome.** The extension acts on an origin only after the user approves it. There is no Add button in its approved-sites list. A site joins only when a consent card is answered while the tab is on that site. The card offers "Allow this action" (one approval), "Decline" and, on some sites only, "Always allow actions on this site". When we read the extension's stored permissions, every approval ever granted was the one-time kind and none was durable. That explained "works, then stops", "connects half the time" and "restarting doesn't help". A one-time approval covered a run of actions on that origin, not just one call. You can't summon the card. When it appears, read its third row: if "Always allow" is there, ask the user to pick it. If it says site-level permissions are disabled, report that as the cause.
- **Read the logs before you theorise.** The "authorization errors" were all per-origin permission denials: no auth failures, timeouts or disconnects in the whole history. Two earlier theories (a session timeout, "a restart fixes it") were guesses that the logs contradicted.
- **Stored approvals can be wiped.** A previously approved origin can silently need approving again. Check the approved-sites list before assuming the user did something wrong.
- **The desktop app's pane has its own consent card**, "Allow Claude to act on <origin>?", with Deny / Always allow / Allow once. It's a browsing safety gate, not a tool permission, so tool auto-approve rules and permission hooks can't answer it. It's per origin, so staging and live domains each need their own approval, and it comes back in every new conversation until "Always allow" is chosen. We lost time chasing it through the tool-approval config.
- **Your browser isn't the user's.** When the user says a setting has no effect, compare their computed values with yours before blaming the cache. A flexbox item with `aspect-ratio` was right in Chrome (Blink) and wrong in Safari (WebKit) at the same width. The fix was `align-self: start`. Believe the pattern in the user's report over your own measurement.
- **Not every overflow is a bug.** A card slider ran past the viewport on purpose, as a cue that there was more to swipe. The textbook `min-width: 0` fix would have removed that cue and resized every card. Check the design intent before you fix something DevTools flags.
- **Favicons are cached hard.** A hard reload doesn't swap the tab icon, and Safari keeps its own favicon cache. Check in a private window or by loading the icon URL directly.
- **CMS caches.** After a deploy, flush the object cache and purge the edge cache, then check the asset's response with `curl`. Otherwise the browser shows the old file and the check means nothing.
- **Large local pages may exceed the pane's preview limit.** A ~700 KB self-contained HTML file wouldn't load in the pane. Open it in a real browser instead.
- **Use screenshots sparingly.** Text and measurements are cheaper and exact. Keep screenshots for what has to be seen (layout, colour, dark mode).

## What it does not cover

Other browsers and real devices: Safari and WebKit, phones, other users' caches and extensions. Anything behind a CAPTCHA, a password prompt or account creation, and purchases or form submissions. Those stay with the user. Approving the browser consent cards is always the user's click. Whether the design looks right is still the user's call.

## Loading this into Claude

> Web changes are verified in a browser before they are reported done. For logged-in or staging sites use Claude in Chrome. If `list_connected_browsers` is empty, ask whether the side panel is open and signed in, in one line, before anything else. For dev servers and local pages use the built-in pane, and set `data-theme="dark"` before any screenshot of a themed page. Read pages as text and measure computed styles at `<breakpoints>` with the JavaScript tool against a baseline taken before the change. Confirm every deployed asset returns 200 with `curl`. When a consent card offers "Always allow" for an origin, tell the user. Never try to answer it yourself.
