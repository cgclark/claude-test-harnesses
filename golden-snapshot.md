# Golden snapshot

> Lets Claude prove that a refactor or data migration reproduces the old output exactly, by freezing what the real code produces before the change and diffing every later phase against it.

**Applies to:** refactors that move data or logic to a new source of truth (hard-coded tables to CSV/JSON,
derived classification to stored fields, name keys to stable ids), in any language · **Needs:** a way to run
the real code and write its output to a file (a debug launch flag, a CLI entry point, or a test), `diff` or a
small compare script

## Why it exists

By default Claude refactors, the build passes, a few screens look right, and it reports "behavior unchanged".
Nothing checks that every item, count and ordering survived. Mismatches turn up later as a drink missing from a
menu or a count that is off by one.

Built for a coffee-machine app whose menu data lived in five places, with classification recomputed on every
render from text scans and hard-coded exception sets. Two definitions of the same machine disagreed and used
different id schemes. The migration ran in six phases, and each one had to diff clean against a Phase-0 snapshot
before it counted as done.

## What it does

1. **Phase 0, no product change:** a debug-only hook runs the real assembly logic with all user state and filters
   off and writes the result as sorted, pretty-printed JSON (lists in display order plus counts). The output is
   committed as `golden-<name>.json`.
2. Each later phase adds a second emitter in the same hook that builds the **same shape** from the new source.
3. Diff the new output against the golden file. Any difference fails the phase.
4. Where the new source feeds something finer than the snapshot captures (wire-level fields, for example), add a
   targeted round-trip gate: `loaded == literal` field by field, written as `{match, diffs}`.
5. When there are two reference definitions, use a reconciliation script that joins them on a key both share
   and reports every disagreement.

## Recipe

**1. Add the snapshot hook** behind a debug flag. It must call the code the app uses, not reimplement it:

```swift
#if DEBUG
func dumpSnapshot() {
    let snap: [String: Any] = [
        "black": ["standard": <realQuery>(.black, .standard).map(\.name), ...],
        "counts": ["blackStd": ..., ...],
    ]
    let url = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
        .appendingPathComponent("snapshot.json")
    try? JSONSerialization.data(withJSONObject: snap, options: [.prettyPrinted, .sortedKeys]).write(to: url)
}
#endif
// at launch:
if ProcessInfo.processInfo.environment["DUMPSNAPSHOT"] == "1" { model.dumpSnapshot() }
```

**2. Capture the golden file before touching anything** (iOS simulator shown; a CLI app just writes to stdout):

```bash
SIMCTL_CHILD_DUMPSNAPSHOT=1 xcrun simctl launch --terminate-running-process <device> <bundle-id> -AppleLanguages "(en)"
sleep 3   # the hook runs once the first screen has loaded its data
DATA=$(xcrun simctl get_app_container <device> <bundle-id> data)
cp "$DATA/Documents/snapshot.json" Fixtures/golden-<name>.json
```

Read it, check the counts against what the user sees on screen, and commit it.

**3. For each phase, emit the new path in the same shape** (`snapshot-new.json`) from the same hook, relaunch,
and diff:

```bash
diff Fixtures/golden-<name>.json "$DATA/Documents/snapshot-new.json" && echo "golden: clean"
```

**4. Gate offline stages too.** If data moves into tables that compile to JSON, the compile script gets a
`verify` step that rebuilds the snapshot shape from the generated file and compares it list by list against the
golden file, plus a round-trip against the app's full export (ids, category, kind, tags, names). Exit non-zero on
any mismatch:

```bash
python3 tools/<catalog_build>.py all     # emit -> compile -> verify; prints mismatches, exit 1 on failure
```

**5. Add a round-trip gate for detail the snapshot omits.** When a bundled resource replaces a source literal,
dump `{resourceLoaded, match, loadedCount, literalCount, diffs}` comparing every field (including byte offsets
and step sizes that only matter on the wire), and keep the literal as a fallback until the gate passes.

**6. Reconcile two references on a shared key.** When two definitions use different id schemes, join on a key
both carry (here, the machine's product code) and report the differences. The report in that migration was short:
the id-namespace split, 2 display names, 1 missing parameter.

## Traps

- **Snapshotting a reimplementation.** If the dump recomputes the menu with its own logic, the golden file tests the
  dump. Call the same functions the views call.
- **Nondeterministic input.** User-created items, live filters, stored ordering and device language all change the
  output. Turn filters off, exclude user content (built-ins only), and pin the language (`-AppleLanguages "(en)"`);
  one simulator defaulted to German.
- **Unsorted output.** Use sorted keys and stable list order so a plain `diff` is meaningful. Compare list order
  too, not just sets, if order is user-visible.
- **Regenerating the golden file to make a phase pass.** The golden file changes only for an intended behavior
  change, recorded as its own commit with a reason.
- **Capturing after the first edit.** Phase 0 is capture only. A snapshot taken mid-change freezes the bug.
- **Joining on names or ids that drift.** Name-derived keys split one person into three entries in the same app.
  Reconcile on a stable key, and migrate stores to stable ids with a one-time, idempotent re-key that keeps orphans.
- **A snapshot proves only what it captures.** Menu lists and counts did not cover wire-format fields; that took a
  separate round-trip gate. Name what each gate covers.
- **Moving view state into data to make the snapshot "complete".** Assembly that interleaves UI state (filters,
  ordering, an add card) stayed in the view on purpose. Centralize the classification predicate it calls, and
  leave the UI state where it is.
- **Debug-only hooks.** The dump runs under `#if DEBUG`. A release-only code path (stripped resources, a fallback
  literal) needs its own check.

## What it does not cover

Visual layout and interaction (whether the screen still looks and behaves right), release-only builds, and
behavior on real hardware (here, whether a brew command still reaches the machine). The human checks the UI and
the device after the gate is clean.

## Loading this into Claude

> Refactors and data migrations here are gated by `Fixtures/golden-<name>.json`, captured from the real code before
> the change. Launch with `DUMPSNAPSHOT=1` (`SIMCTL_CHILD_DUMPSNAPSHOT=1 xcrun simctl launch ... -AppleLanguages
> "(en)"`), then diff the emitted snapshot against the golden file; for table changes run
> `python3 tools/<catalog_build>.py all`. A phase is done only when the diff is clean. Never regenerate the golden
> file to make a diff pass; change it only for an intended behavior change, in its own commit.
