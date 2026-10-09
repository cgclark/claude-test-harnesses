# Baseline parity

> Lets Claude show that an app ported to a new platform still reads and writes the original app's data the way the original does, by diffing the port's database against a frozen baseline from the original and logging every intended divergence.

**Applies to:** rewrites and ports that share a data file or database with an original app (desktop → tablet, one
framework → another), where the original stays in production · **Needs:** a copy of the original's data taken before
the port touched it, `sqlite3` 3.31+ (for `sha3()`) or the equivalent dump tool for your database, read access to
the original app's source

## Why it exists

By default Claude ports screens, the new app runs against the data, and it reports "same data, works". Nothing
shows whether the port changed rows, dropped a table's triggers, or behaves differently on save. A port that will
later be ported back has a second problem: every change that is not written down is lost.

Built for an iPad rewrite of a Windows materials-library app. The two share no code, only the SQLite file exported
from the original's SQL Server database. Divergences the log had to capture:

- The legacy file carried SQL-Server-style foreign-key triggers that are invalid in SQLite (`sub-select returns 2
  columns`) and blocked every insert. Dropping them was a data change that affects the original app too.
- Seeding five new languages added about 325 translation rows, filled from English.
- The original deletes the translation rows of an entry whose names are all empty on save; the port kept them. That
  was a behaviour the port lacked, found by reading the original's save command.

## What it does

1. Freeze the original's data once, before the port writes anything: `baselines/<db>-baseline-<yyyymmdd>.db3`.
2. After a change, diff the port's working copy against the baseline: schema, then row counts per table, then rows
   (blobs reduced to length and hash).
3. Every difference is either an intended change, logged in the parity file, or a bug.
4. For behaviour (limits, save rules, validation), read the original's source and record "parity confirmed" or
   "open divergence" with where in the original it lives.
5. The parity file carries a "last synced to vX.YY" line that is bumped before a change counts as done.

## Recipe

**1. Freeze the baseline.** Copy the data file with no writer open, and keep it read-only:

```bash
mkdir -p baselines
cp <original-data>.db3 baselines/<db>-baseline-$(date +%Y%m%d).db3
chmod a-w baselines/*.db3
```

**2. Get the port's working copy.** For an iOS simulator:

```bash
DATA=$(xcrun simctl get_app_container <device> <bundle-id> data)
cp "$DATA/Documents/<db>.db3" /tmp/working.db3      # quit the app first, or copy -wal and -shm too
```

**3. Diff schema and counts:**

```bash
B=baselines/<db>-baseline-<date>.db3; W=/tmp/working.db3
diff <(sqlite3 -readonly "$B" .schema) <(sqlite3 -readonly "$W" .schema) && echo "schema: same"
for t in $(sqlite3 -readonly "$B" "SELECT name FROM sqlite_master WHERE type='table' AND name NOT LIKE 'sqlite_%'"); do
  echo "$t $(sqlite3 -readonly "$B" "SELECT count(*) FROM $t") $(sqlite3 -readonly "$W" "SELECT count(*) FROM $t")"
done
```

**4. Diff rows**, ordered by primary key, with blobs hashed so the output stays readable:

```bash
Q="SELECT <Key>, <Type>, <ValueA>, <ValueB>, length(<Blob>), hex(sha3(<Blob>)) FROM <Table> ORDER BY <Type>, <Key>"
diff <(sqlite3 -readonly "$B" "$Q") <(sqlite3 -readonly "$W" "$Q")
```

Do this per table. A clean diff after a UI-only change is the pass. After a data change, every line in the diff
must match an entry in the parity file.

**5. Keep the parity file** (`PARITY-WITH-<ORIGINAL>.md`) with three markers and two lists:

```markdown
Last synced to <port> **v<x.yy>**.

## ★ PORT — new behaviour to carry back to the original
## ◑ DATA — changes to the shared data file (both apps see them)
## ○ Port-only — platform plumbing with no equivalent in the original (do not port)
### Parity confirmed (no divergence) — e.g. "names have no length limit: no MaxLength in <view>, none in <model>"
### Open divergence — the original has it, the port does not (with the original's file and command name)
```

Each entry says what changed, where in the port, and what porting it back would touch.

**6. Give the port a reset to the baseline.** Restore the working file from a bundled or saved reference: close the
database handle first so the WAL is checkpointed, delete `<db>`, `<db>-wal` and `<db>-shm`, copy, reopen. This makes
every test start from the same data.

## Traps

- **Copying a live SQLite file.** With WAL mode, recent writes sit in `-wal`. Close the handle (or quit the app)
  before copying, and remove stale `-wal`/`-shm` next to the destination before restoring.
- **Template and placeholder rows.** The legacy data pre-creates about 100 empty rows per type, and its first rows
  are "select …" templates. The port must show only what the original shows. Compare counts of what the user sees,
  not raw row counts alone.
- **Triggers from another database engine.** A schema converted from SQL Server can contain triggers that fail in
  SQLite and block writes. Test an insert, not only reads.
- **Backfills are data changes.** Filling blank names from English, or seeding new languages, changes rows the
  original reads. Log them under ◑ DATA.
- **Assets ported as-is.** The original's default image was an empty file, and the port copied it. Diff assets by size
  and hash, as well as rows.
- **Only logging one direction.** Reading the original's save path found behaviour the port lacked. Record those as
  open divergences, not as port features.
- **Debug and Release installs.** The generated scheme built one configuration while the install picked up the other,
  so the old app ran against the data. Pass `-configuration` explicitly and check the binary's mtime before trusting
  a result.
- **"Last synced" left behind.** If the version line is not bumped, the next session cannot tell which changes are
  logged. Treat the bump as part of done.

## What it does not cover

Whether the original app still runs correctly against a file the port has changed (that needs the original running,
here on Windows), visual parity with the original's screens, and any live database sync. A person checks the
original against the changed file. For exact-output checks inside one codebase, see
[Golden snapshot](golden-snapshot.md). A related dev-time check for line breaking in space-less scripts is in
[Translation lint](translation-lint.md).

## Loading this into Claude

> The original app's data is frozen in `baselines/<db>-baseline-<date>.db3`. After any change that writes data, diff
> the working copy against it (schema, per-table counts, rows with blobs hashed) and account for every difference in
> `PARITY-WITH-<ORIGINAL>.md` under ★ PORT, ◑ DATA or ○ Port-only. Check behaviour against the original's source and
> record parity confirmed or open divergence. Bump the "Last synced" line before calling a change done. Never
> overwrite the baseline.
