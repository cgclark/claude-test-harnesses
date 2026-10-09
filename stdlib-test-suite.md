# Standard-library test suite

> Lets Claude prove every change to a dependency-free Python tool in about two seconds with one command, and exit non-zero on the first regression, without adding pytest or anything else the tool promises not to need.

**Applies to:** small Python tools and libraries that ship as "standard library only" · **Needs:** Python 3.7+, and
whatever real data files the tool ships with (word lists, fixtures)

## Why it exists

When a tool's selling point is "no dependencies", adding pytest just for testing breaks the promise. So by default
Claude ends up testing by hand: run the CLI, look at the output, say it works. Every later change then reruns
nothing, and features built across several sessions regress silently.

Built for a crossword-construction toolkit (binary and JSON puzzle formats, grid generation, a backtracking fill,
an HTTP server and a browser constructor). The worst bug it now guards was a fill that looked fine: a slot
completed only by its crossing words was never checked, and a noisy word list hid the non-words that resulted.
The check "every entry is a dictionary word" catches that on every run. The suite grew with the tool, from 76 checks
to 108 today, one block per feature.

## What it does

1. One file, `tests.py`, at the repo root, imports the package straight from the source tree.
2. A five-line `check(name, cond)` helper prints `ok` or `FAIL` per check and counts both.
3. Checks are grouped by feature, top to bottom, sharing a few fixtures built once (a tiny hand-made word list, the
   real shipped list, a 5x5 grid).
4. The last line prints `N passed, M failed` and exits 1 if anything failed, so it works as a gate in scripts, hooks
   and CI.

## Recipe

**1. The harness**, in full:

```python
"""Self-contained checks for <pkg>. Run: python3 tests.py"""
import os, sys
sys.path.insert(0, os.path.dirname(os.path.abspath(__file__)))   # test the source tree, not an installed copy

PASS = FAIL = 0
def check(name, cond):
    global PASS, FAIL
    if cond: PASS += 1; print("  ok   " + name)
    else:    FAIL += 1; print("  FAIL " + name)

# ---- <feature> -------------------------------------------------------
from <pkg>.<module> import <Thing>
...
check("<what must be true, in words>", <expression>)

print("\n%d passed, %d failed" % (PASS, FAIL))
sys.exit(1 if FAIL else 0)
```

**2. Write checks as plain expressions over real outputs.** Which kinds to cover:

- **Round trips** for every file format: write → read → compare grid, title, a clue; convert A → B → compare.
- **Format invariants** you can check from the bytes: magic string at its offset, header width, clue count.
- **Properties, not snapshots,** for search output: "filled", "every entry is a word", "no duplicates", "budget
  never exceeded", "symmetric", "no unchecked cells", "connected". Loop them over sizes and seeds.
- **Determinism:** the same input with no seed gives the same output twice.
- **Safety:** the server's name resolver rejects `../../etc/passwd` and non-puzzle extensions. Use `tempfile.mkdtemp()`
  for anything that writes.
- **Generated HTML:** it starts with `<!doctype html>`, has no external `src=`/`http://` refs, and contains the ARIA
  roles, endpoints and handlers the page needs. These are string checks, cheap and blunt.

**3. Bound every search.** Each fill gets `time_limit=` (10-20 s) so a pathological case fails one check instead of
hanging the run.

**4. Run it** after every change, before saying it works:

```bash
python3 tests.py            # ~2 s; last line "N passed, 0 failed"; exit code 0
python3 tests.py | grep FAIL
```

**5. One check per fixed bug.** When a bug is found, add the check that would have caught it, see it fail, then
fix.

## Traps

- **Testing an installed copy.** Without the `sys.path.insert`, `import <pkg>` may pick up an older installed
  version and pass. Put the source tree first.
- **Vacuous passes.** `check("budget never exceeded", (not r.ok) or r.junk <= 2)` passes when the fill fails. That's
  right for a budget that may be infeasible, but pair it with a check that the uncapped case does fill, or the block
  can go all-green while doing nothing.
- **Tests that depend on licensed data.** The fill checks load the real shipped word list (CC BY-NC-SA). Lists
  under personal-use licences, and clue data derived from a copyrighted corpus, are git-ignored. Keep the suite on
  the redistributable list only, or a fresh clone fails.
- **A tiny hand-made list hides correctness bugs.** The incidental-completion bug only showed with a real 300k-word
  list. Use both: the tiny list for exact ranking checks, the real one for properties.
- **"Different seeds give different fills" is not guaranteed.** Assert that both seeded fills are valid, not that
  they differ.
- **String checks on HTML prove wiring, not behaviour.** "/api/fill in page" doesn't mean the button works. After UI
  changes, also run the page in a browser (or at least `node --check` the extracted script).
- **Server pages built at import time.** The running server keeps the old page after an edit. The suite imports
  fresh, so it passes while the live server is stale. Restart the server before checking by hand.
- **External validators stay outside.** The binary format was cross-checked once against a third-party reader. That
  check is not in the suite, which would need the dependency. Record it in the README and rerun it by hand when the
  writer changes.

## What it does not cover

Fill quality (whether the words are good, not just valid), real browser interaction in the constructor, TLS against
real clients, and performance beyond "finishes inside the time limit". Those are judged by the human or checked
separately.

## Loading this into Claude

> `python3 tests.py` is this project's gate: run it after every change and before saying anything works. It must
> end `N passed, 0 failed` and exit 0. It has no dependencies; keep it that way (no pytest). New feature → new
> `# ---- <feature> ----` block of `check("<plain statement>", <expr>)` lines. Fixed bug → a check that fails
> without the fix. Bound every search with a time limit. Don't make the suite depend on git-ignored or
> personal-use data.
