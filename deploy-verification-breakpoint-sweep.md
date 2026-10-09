# Deploy verification and breakpoint sweep

> Lets Claude prove that a theme deploy landed whole and that the rendered site did not move at any width it did not mean to change, instead of reporting "deployed" because `scp` returned 0.

**Applies to:** WordPress themes and other server-rendered sites deployed over SSH/SFTP, plus scripted edits to CMS page content (built for a WordPress block theme) · **Needs:** key-based SSH to the host, `md5`/`md5sum` on both ends, `wp-cli` on the server, `sass` (Dart Sass) if the theme compiles SCSS, a browser Claude can measure in (see [browser-driving.md](browser-driving.md)), and a person with Safari for the WebKit check

We built this harness. The browser side (surfaces, consent cards, the measuring probe, dark mode) is in [browser-driving.md](browser-driving.md) and is not repeated here.

## Why it exists

Without it Claude copies files, sees no error, and says it's done. Each of these got past that:

- Uploaded files arrived with mode `600`. The web server returned 403 for the stylesheet and the whole site was unstyled.
- A deploy that sends PHP and CSS separately can stop halfway. The template then emits markup the stylesheet doesn't know about, and nothing errors until someone loads the page.
- The compiled stylesheet had been hand-patched for months while the SCSS was edited separately. Source and build disagreed in both directions, so "rebuild from source" would have silently reverted live work.
- Two layout bugs existed only between 991 and 1160 px, invisible at the 1440 and 375 px Claude had checked.
- A layout was right in Chrome and wrong in Safari at the same width (`aspect-ratio` on a flex item; WebKit lets the flex stretch win). Claude measured its own browser, said "it works", and blamed caching.
- A scripted page edit through `wp_update_post()` without `wp_slash()` stripped one level of backslashes and corrupted block JSON on four pages. A later edit shrank a page by ~1.9 KB, which looked like data loss and wasn't (save-time markup normalisation).

## What it does

1. **Deploy as one unit.** A script refuses to send anything unless every named file exists, uploads to a temp dir, lints PHP there, then installs all files in one remote command with `chmod 644`, and flushes caches.
2. **Verify by hash.** Every deployed file's md5 on the server is compared with the local copy. Any mismatch fails the deploy. `curl` confirms each asset returns 200.
3. **Sweep fixed widths.** The same measuring probe runs at a fixed list of widths before and after the change. The two outputs are diffed. Pass = identical except where the change was meant to differ.
4. **Cross-engine check.** For anything the user reports as "has no effect", compare their computed values in Safari with Claude's in Chrome at the same width before theorising.
5. **Guard content writes.** Dump the page content to a file before a scripted write. After it, compare block count, broken block attributes, paragraph count and escape counts, not byte length.

## Recipe

### 1. Deploy script

Put SSH connection details in `~/.ssh/config` under one alias, not in the script. Keeping the user name and host in one place stopped them being confused with the site's own hostname.

```text
Host <ssh-alias>
  HostName <sftp-host>
  User <sftp-user>
  IdentityFile ~/.ssh/<deploy-key>
```

The script's shape (ours is `deploy.sh` in the theme root, bash, `set -euo pipefail`):

```bash
./deploy.sh [--build] <path> [<path> ...]      # paths relative to the theme root, structure kept on the server
./deploy.sh --build assets/build/main.min.css functions.php
```

What it does, in order. Each step is there because of a failure above.

```bash
# 0. --build: compile, then copy into the directory the theme actually enqueues from.
#    A compile that is not copied changes nothing on the front end.
sass --no-source-map --style=compressed <scss-entry> <compiled.css>
cp <compiled.css> <enqueued-build-dir>/main.min.css
md5 -q <enqueued-build-dir>/main.min.css | cut -c1-12      # the cache-buster the page should request

# 1. Every named file must exist before anything is sent.
for f in "${files[@]}"; do [[ -f "$f" ]] || exit 1; done

# 2. Upload to a remote temp dir, not the theme.
ssh <ssh-alias> "mkdir -p /tmp/<stamp>/$(dirname "$f")"
scp -q "$f" "<ssh-alias>:/tmp/<stamp>/$f"

# 3. Lint PHP where it sits. A parse error in functions.php is a white screen on every URL,
#    wp-admin included, and the fix has to come back over this same connection.
ssh <ssh-alias> "set -e; php -l /tmp/<stamp>/functions.php"

# 4. Install everything in ONE remote command so set -e stops before a partial install
#    and before any cache flush. chmod 644 every file: scp'd files arrive 600 and nginx 403s them.
ssh <ssh-alias> "set -e; cp /tmp/<stamp>/$f <theme-dir>/$f; chmod 644 <theme-dir>/$f; ...; \
  rm -rf /tmp/<stamp>; wp cache flush; echo y | wp edge-cache purge --domain=<staging-domain>"

# 5. Verify every file by md5, local against server. Any difference = "deploy incomplete", exit 1.
local_md5=$(md5 -q "$f" 2>/dev/null || md5sum "$f" | cut -d' ' -f1)
remote_md5=$(ssh <ssh-alias> "md5sum <theme-dir>/$f | cut -d' ' -f1")
```

`wp edge-cache purge` is specific to WordPress.com hosting. It prompts y/n and has no `--yes` flag, hence `echo y |`. On other hosts, use that host's purge.

Then from outside any browser cache:

```bash
curl -sI "https://<staging-domain>/wp-content/themes/<theme>/assets/build/main.min.css" | head -1   # expect 200
curl -s  "https://<staging-domain>/" | grep -o 'main.min.css?ver=[0-9a-f]*'                        # expect the new hash
```

### 2. Build from source, never patch the build

If the compiled CSS and the SCSS have drifted, don't pick one. Reconcile toward what is **live**: take the computed-style sweep (step 3) of the live site as the baseline, rebuild from source, deploy to staging, and sweep again until the outputs match exactly. Then only ever edit source. If two stylesheets share partials (front end and block editor), rebuild and deploy both together.

### 3. Breakpoint sweep

Use the measuring probe from [browser-driving.md](browser-driving.md#recipe) (step 4), extended into a per-section fingerprint: hash each section's box plus `padding`, `margin`, `max-width`, `display`, `align-items`, `row-gap`, `font-size`, `line-height` for a fixed selector list. Comparing hashes per section shows where a change spread, not just that it did.

```js
// illustrative: our fingerprint was run ad hoc, not kept as a file
const P = ['padding','margin','max-width','display','align-items','row-gap','font-size','line-height'];
[...document.querySelectorAll('<section-selector>')].map((s, i) => {
  const els = [s, ...s.querySelectorAll('<selector-list>')];
  const rows = els.map(e => { const r = e.getBoundingClientRect(), c = getComputedStyle(e);
    return [r.x, r.y, r.width, r.height].map(v => v.toFixed(1)).join(',') + '|' + P.map(p => c[p]).join('|'); });
  return { i, n: els.length, sig: rows.join('\n') };   // diff sig strings before vs after
})
```

Widths: choose every breakpoint the theme declares, plus one on each side of it. Ours were **375, 768, 990, 991, 1000, 1100, 1160, 1440**. Two bugs lived only between 991 and 1160.

Per width:

1. Set the viewport (`resize_window` in either browser tool).
2. **Navigate again after resizing.** A responsive image chosen at the old width inflates a section and reads as a regression.
3. **Wait for the page to settle** (fonts, sliders, lazy images) before probing. An immediate probe once read a page 546 px short.
4. Run the probe, save the output to a file named by width and phase (`before-768.json`).

**A/B against the real baseline.** To separate "my change" from "already like that", deploy the pre-change theme files (from a git tag) against the current database, sweep, restore the new files, and sweep again. Check the tag predates the change. An A/B against a commit that already contained it let one regression through.

### 4. Chrome against Safari

We had no automated Safari driver. The check was: when the user says a setting does nothing, ask them for the computed value from Safari's Web Inspector (element, then Computed) for the named element at their window width, and compare with Chrome's at the same width. Two engines disagreeing at one width points at an engine difference, such as WebKit's flex stretch beating `aspect-ratio` (fix: `align-self: start` on the ratio'd item). Same values in both engines but wrong for the user points at a rule that doesn't reach their case, such as a rule nested inside one block style variant that the other variant never gets.

`safaridriver` (ships with macOS) could automate this. We did not use it, so it is not verified here.

### 5. Content writes through wp-cli

Before any scripted write, dump the content yourself. Revisions are not a rollback: after one scripted edit the page had exactly one revision, holding the post-change content.

```bash
wp post get <id> --field=post_content > page-<id>.html          # per page, immediately before the write
wp db export /tmp/<name>.sql --add-drop-table && gzip /tmp/<name>.sql   # whole DB; scp down, then rm on server
```

Write with `wp_slash()`, from a PHP file run with `wp eval-file`, not inline `wp eval`. Shell quoting mangles regex backslashes and gave false damage reports on healthy pages.

```php
// <write>.php  — run: wp eval-file <write>.php
$old = get_post( <id> )->post_content;
$new = /* the edit */;
// abort unless the edit's anchor matched exactly once, and escapes survived
if ( substr_count( $new, '\\u003c' ) !== substr_count( $old, '\\u003c' ) ) { WP_CLI::error( 'escape count changed' ); }
wp_update_post( array( 'ID' => <id>, 'post_content' => wp_slash( $new ) ) );
```

After the write, compare these against the dump. Don't use byte length: save-time normalisation changed one page by about 1.9 KB while two others gave byte-exact deltas.

- block count (`count( parse_blocks( $c ) )`, recursively) and block-comment count
- blocks whose attribute JSON fails to decode
- paragraph count and rendered text (`wp post get <id> --field=post_content` vs the page's visible text)
- damage marker: a bare `u003c` not preceded by a backslash in `post_content`

Restore one page from its dump (still through `wp_slash()` if done in PHP):

```bash
wp post update <id> --post_content="$(cat page-<id>.html)"
```

We wrote these PHP checks ad hoc each time and didn't keep them. The snippets above are a sketch of what they checked, not a saved script.

## Traps

- **`scp` file modes.** Files land `600` on some hosts and the web server answers 403. `chmod 644` in the install step, then `curl -sI` for a 200. A browser with the old file cached will not show the failure.
- **Compiled-but-not-copied.** If the theme enqueues from a build directory and hashes that file for the cache-buster, compiling elsewhere changes nothing. Print the expected `ver=` hash at build time and grep the served page for it.
- **Cache-buster is a content hash.** If the `ver=` on the page did not change, the file on the server did not change. Check that before blaming the browser cache.
- **Breakpoints are spread across files.** Our nav's mobile switch lived in three partials (nav, header, search) through one mixin, and the burger rode the same mixin. Moving one file left a band with no menu at all. Grep for the breakpoint value across all partials before moving it.
- **Block ids that are hashes of attributes.** A page-section block's element id was derived from its attributes, so CSS pinned to the id stopped matching after any edit, with no error. Emit such rules at render time (a `render_block` filter) instead.
- **CMS options persist past defaults.** Once an ACF options page is saved, changing a field's default in code has no effect. Change the stored option (`wp option update options_<field> <value>`).
- **"Fixing" deliberate overflow.** A card slider overflowed the viewport on purpose (the peek cue). See [browser-driving.md](browser-driving.md#traps).
- **A comparison that compared nothing.** A theme-archive check reported "identical" when the extraction had aborted on an empty glob and a filter swallowed the error. Print the count of files compared.
- **`Element.matches()` throws on `:has()`-heavy selectors.** A sweep of `document.styleSheets` asking which rules match an element silently returned almost nothing. The DOM gives the computed value, not the rule that produced it. Read the source for that.

## What it does not cover

Safari, Firefox and real phones are checked by a person. This harness only compares numbers they report. Whether the design looks right. Other users' caches, extensions and zoom levels. The host's own backups and restore tools. Production deploys, if they need someone's sign-off. Credentials: if key auth stops working, a person fixes access. Claude does not type passwords.

## Loading this into Claude

> Deploy theme files only with `./deploy.sh [--build] <paths>`. It installs all-or-nothing, sets `chmod 644`, purges caches and md5-verifies every file against the server. A deploy is done only when every file says `ok`, each asset returns 200 to `curl -sI`, and the served page carries the new `ver=` hash. Edit SCSS, never the compiled CSS. For any CSS or template change, save a fingerprint at `<widths>` before the change and diff it after. Navigate again after each resize and let the page settle first. When the user says a setting has no effect, ask for their Safari computed values before theorising. Before any scripted content write, dump `post_content` to a file. Write through `wp_slash()` from `wp eval-file`. Judge the result by block count, broken attrs, paragraph count and escape counts, not bytes.
