# Booking dry run

> Lets Claude drive a third-party booking portal through every step of a reservation, reading the live page at each one, and stop before the final confirm, so a booking flow can be built and re-tuned without placing a booking.

**Applies to:** automation of web portals you don't control: reservation, booking or ordering flows behind a login (built for a residential amenity-booking portal) · **Needs:** Google Chrome with a dedicated profile started with `--remote-debugging-port`, Node 22+ (global `WebSocket` and `fetch`, no npm), a person to sign in to that profile, and a person to place any real booking

We built this harness. For the general rules of driving a browser (Claude in Chrome vs the built-in pane, site consent cards, reading pages as text), see [browser-driving.md](browser-driving.md). This page covers a scripted Chrome DevTools Protocol (CDP) driver for one portal.

**Confirming or submitting stays with a person.** The dry run ends on the confirmation page. Claude does not click Confirm, Submit, Book or Pay, does not tick the terms checkbox that gates them, and does not pass a flag that would. A real booking is placed by the person whose account it is, or by an unattended executor they set up and started themselves. Claude never answers a native `confirm()` dialog on their behalf.

## Why it exists

The portal changes without notice and its markup is hostile to scripting: one month view rendered as 28 nested tables, buttons that are DevExpress `<input>` controls with no text content, popups instead of page loads, a week grid where table indexes landed on the wrong column. Selectors written from a guess failed silently. The first version of the booking script had several wrong ones and could not have booked anything.

Without a dry run, the only way to learn whether a step works is to place a real booking, which then has to be cancelled. A dry run gives Claude the live page's state at each step, so it can fix the step that broke and leave the last one to a person.

## What it does

1. **Attach** to a Chrome the person has already signed in to, over CDP on a local port. No credentials go through the script.
2. **Walk the flow** one step at a time (switch account, open the calendar, pick the amenity, set guests, find the slot), logging what each step found.
3. **Dump on failure.** When a step can't find its target, print the page's visible text (first ~400 characters) and the counts of the controls it looked for, then stop.
4. **Stop before confirm.** Pass = the flow reached the confirmation page with the right date, time and details showing. The script exits there.
5. **Read live data separately.** A read-only snapshot script parses the live calendar month by month and prints it (`--dry`), which proves the read selectors without publishing or booking anything.

## Recipe

### 1. A dedicated, person-signed-in Chrome

Start a separate Chrome profile with a debugging port, so the user's everyday browser is untouched:

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --remote-debugging-port=<port> \
  --user-data-dir="<data-dir>/chrome-profile" \
  "<portal-url>"
```

The person signs in to the portal in that window and leaves it running. The cookies persist in the profile across restarts. Check it is reachable:

```bash
curl -s http://127.0.0.1:<port>/json/version     # expect a JSON object with webSocketDebuggerUrl
```

### 2. A small CDP driver

Ours (`portal.js`, about 120 lines) attaches to the existing portal tab and exposes `eval`, `goto`, `waitFor(expr)`, `click(sel, text)`, `select(sel, value)`, `fill(sel, value)`, `exists`, `text` and `signedIn()`. Design points that mattered:

- Drive through `Runtime.evaluate`: element `.click()`, set `.value` then dispatch `input` and `change`. **Never synthetic pixel mouse events.** They miss when the window is in the background or headless.
- `waitFor` polls a JavaScript condition every 250 ms with a timeout and a label. A timeout names what never appeared, so the failure says which step broke.
- `signedIn()` checks the page for the signed-in marker. If the session has expired, the script stops and tells the person to sign in again. It doesn't try to sign in.

### 3. The drive script

One hard-coded request at the top (date, start, end, guests, amenity), then each step in order:

```bash
node portal-book-drive.js            # walk the flow, log each step, stop before confirm
```

Each step logs what it saw, for example `{"reserveNowCount":2,"amenities":[...]}` or `{hasGuests:true, selects:1, tables:N}`, so Claude can compare the page with what the step expected.

Our file also accepts `--confirm`. **As it stands on disk it walks only as far as the guest count and slot grid, and `--confirm` just prints that the confirm steps aren't wired.** The remaining steps (pick the slot, set the end time, Next) were tuned with a person present and then moved into the booking module the executor uses. For a new portal, wire the steps up to the confirmation page only. Claude never passes `--confirm`. If a confirm path exists at all, a person runs it.

Patterns that made the steps reliable, from that tuning:

- **Match controls inside their row.** Find the row whose text contains the amenity name, then the button inside it by id prefix (`[id^=btnReserveNow]`). A button whose label is in `value`, not `textContent`, never matches a text search.
- **Click grids by geometry.** Find the day-header cell for the date and the time-label cell for the start time (shortest element whose whitespace-normalised text matches), take header-x by row-y, `document.elementFromPoint(x, y)`, climb to the slot cell (`.availableSlot`) and `.click()` it. If the cell there isn't an available slot, report its class. That is how "slot taken" shows up.
- **Normalise whitespace before matching.** A header rendered as `Thu,\nSep 10` doesn't contain `Sep 10` until `\s+` becomes one space. Without that, the week-paging loop skipped past the right week.
- **Wait for the grid's cells, not its container.** The guest dropdown rendered before the slot cells. A probe run between the two concluded the date wasn't visible and paged away from the current week.
- **Wait on elements, not text.** An `<input>` button's value isn't in `document.body.innerText`.

### 4. Live selectors from a read-only snapshot

`publish-snapshot.js` reads the live calendar and never books:

```bash
node publish-snapshot.js --dry 6     # parse 6 months and print a sample; publishes nothing
```

When the DOM is unparseable, parse `innerText`. Ours found the smallest element containing the weekday header row, split its text into lines, and walked them. A bare number line is a day, then a time-range line and an amenity-name line make an entry. It got right:

- **Month spillover.** Skip lines until the first bare `1`, and stop when a day number drops below the previous one. Otherwise the next month's leading days are attributed to this month.
- **Truncated days.** The grid shows "Show more" on busy days. Record those days as truncated rather than as having only the visible entries.
- **Sentinel values.** `12:00 AM To 12:00 AM` meant a blocked day, not a midnight booking.

Run the dry snapshot after any portal change you suspect. If its counts drop to zero, the read selectors broke before any booking step did.

### 5. Offline logic tests

Keep validation separate from the browser so it can be tested with no network:

```bash
node executor.js selftest     # sample requests through the guardrails: conflict, bad unit, too long, past date, dedupe
```

### 6. The local-tool test plan

`TEST-PLAN.md` is a supervised, step-by-step check of the project's own local booking tool (browser `localStorage`, no portal): create, delete, recreate with different details, edit, clean up. Each step says exactly what to click and what to expect. The key assertion is that **editing replaces the entry: the count stays at 1**, not 2. A person approves each step or clicks it while Claude checks the result. Use the same layout for a portal plan: one test date with nothing on it, explicit expected text per step, and a cleanup step.

## Traps

- **Pixel clicks.** Synthetic mouse events missed in a background or headless window. Use element `.click()` and value-set throughout.
- **Account switching back to back.** Running account switches one after another left a half-open modal that broke the next one and signed the session out. Wait for the switch popup's target row to render, retry opening it, and check the active account afterwards.
- **Session expiry mid-run.** The dedicated profile signed out on its own several times. Check `signedIn()` first, and stop with a clear message if it fails. Signing in again is the person's job.
- **Autofill doesn't fire on scripted focus.** Chrome only autofills a login form after a real input event, not after JS `.focus()`. Don't work around this by typing credentials. Ask the person to sign in.
- **Table indexes lie.** In the week grid, index-based cell lookup landed on column 0. Geometry from the header and time-label cells was right.
- **Two writers to one calendar.** The live executor once published its local simulator data over the real calendar snapshot, and the app showed a blank calendar. A dry or simulated mode must never write to the same output as the live reader.
- **Memory notes go stale.** A note said the booking module was "not yet updated" with the tuned selectors, but the file on disk had been. Read the scripts, not the notes.

## What it does not cover

Placing, confirming, paying for or cancelling real bookings: a person does these, or an executor they started deliberately. Signing in, passwords, one-time codes, CAPTCHAs and accepting the portal's terms all stay with a person. Whether the portal operator permits automation is the account holder's call. Other people's accounts are out of scope.

What we did not verify for this page: we didn't run `portal-book-drive.js`, `publish-snapshot.js --dry` or `executor.js selftest` while writing it, because the first two need a live, signed-in session on a third-party portal. Commands and flags are taken from the scripts' own code and usage comments.

## Loading this into Claude

> To work on the `<portal>` booking flow, use the dry run. Attach to the dedicated Chrome on `127.0.0.1:<port>` that the user has signed in to, run `node <drive-script>`, and read each step's log. If a step fails, fix that step's selector from the page dump. Stop at the confirmation page. Never click Confirm, Submit, Book or Pay, never tick the gating terms box, never pass `--confirm`, and never override `window.confirm`. Say the flow is ready and let the user place the booking. If the session has expired, ask the user to sign in again. Never type credentials. After portal changes, run `node <snapshot-script> --dry` to check the read selectors still parse.
