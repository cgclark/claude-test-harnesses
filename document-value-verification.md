# Document value verification

> Lets Claude confirm that a date, amount or name it is about to quote actually appears in the source document's extracted text, and tell a real "not in the document" from a document that was never indexed.

**Applies to:** any work where Claude quotes values from a set of documents (PDF scans, email, Office files, images)
that it read through an extraction pipeline rather than in full · **Needs:** a local index of extracted text per
document (here Dossier: Python 3, SQLite FTS5, Apple Vision OCR on macOS), the original files on disk

## Why it exists

By default Claude reads a document, or a summary of one, and writes "the invoice total is $1,250.00". Nothing checks
that the string is in the source. On-device summaries help triage but are a reduction: in testing one transcribed a
dollar figure imperfectly. A long document read in context is also expensive, and summaries drift.

The second failure is worse. When a search finds nothing, that reads as "the document does not say this". In a gap
analysis, where the whole question is what a document does not say, a document that was never indexed turns into
"confirmed absent". Dossier's ingest failed silently three ways, each reporting success.

Built for document-heavy review work, with a small made-up fixture for the recipe below.

## What it does

1. Ingest extracts text per document (text layer, OCR, email headers and body, Office XML) into sidecars and a
   full-text index, and records every extraction failure in a `gap` table.
2. `find` searches the index and returns ids with a short snippet (plus an on-device gist, labelled not
   authoritative). No document text beyond the snippet enters the context.
3. `verify <value> <id>` checks the exact string against that document's extracted text and returns
   `present`, `count` and character offsets.
4. `get <id> <a> <b>` (or `--pages`) pulls only the slice around a hit when the context matters.
5. Before treating a no-hit as absence, check the document has text and no open gap.

## Recipe

**1. Build a made-up fixture** and ingest it into a scratch work dir:

```bash
mkdir -p fixture && printf 'Invoice INV-0042\nIssued 3 March 2026\nTotal due: $1,250.00\n' > fixture/invoice.txt
dossier ingest fixture --work work
```

**2. Find, verify, slice:**

```bash
dossier query work find "1,250.00"          # → [{"id": 1, "doc": "invoice.txt", "snippet": "…Total due: $[1,250.00]"}]
dossier query work verify '$1,250.00' 1     # → {"present": true, "count": 1, "offsets": [48]}
dossier query work verify '$1250.00' 1      # → {"present": false, ...}  exact match only
dossier query work get 1 0 2                # lines 0–1 of the extracted text
dossier query work get 1 6 9 --pages        # pages 6–9 (needs "===== PAGE n =====" markers)
```

Quote a value only after `verify` returns `present: true` against the document you cite. Quote it the way the
document writes it.

**3. Rule out silent failure before reporting absence.** For the document in question:

```bash
sqlite3 work/manifest.db "SELECT gap_type, detail FROM gap WHERE artifact_id=<id> AND status='open'"
sqlite3 work/manifest.db "SELECT a.bytes, length(f.body) FROM artifact a JOIN doc_fts f ON f.artifact_id=a.id WHERE a.id=<id>"
```

An open gap (`no-text`, `ocr-error`, `r1-timeout`, `sparse-ocr`), or a few hundred characters from a large file, means
"not indexed", not "not there". Then confirm the search works on that document by finding a word you know it
contains. Only then report the value as absent, and name the check you ran.

**4. Read the ingest summary every time.** It prints artifact counts and a warning line when files errored or produced
no text. A run that reports `artifacts: 0` is a failure, whatever the exit code.

**5. Measure the context saving** if you need to justify the pipeline:

```bash
dossier savings work
```

It prints the estimated Claude tokens for two baselines (pages as images at ~1,600 tokens each; full text at
characters/4) against the index's own cost, and on-device model tokens as a separate figure that is never summed
with Claude tokens.

## Traps

- **A `sources/` subfolder hijacks the ingest.** If the folder you point at contains a `sources/` directory, only that
  is read. A drop folder with a leftover `sources/` holding only `.DS_Store` ingested nothing and reported
  `artifacts: 0`, exit 0 (reproduced). Stage files into a clean folder first, top-level files only.
- **Near-empty extraction counts as success.** `textutil` rejected one valid `.docx` ("isn't in the correct format")
  and wrote 99 bytes for a 112 KB document; the artifact was recorded and every `find` returned no hits. Empty
  output now lands in the `gap` table, but trivially short output does not. Compare text length with file size.
  Parsing the OOXML directly (`w:t` elements, including table cells) recovered the text.
- **Unsupported extensions are skipped without a trace.** WebP images were not in the image list and disappeared
  until `.webp` was added; failures are now recorded as gaps. After adding a format, re-check the counts.
- **Re-running does not repair.** Ingest skips files whose hash is already in the manifest, so a document indexed
  with missing text stays that way. Re-extract it and replace its index row, or ingest into a fresh work dir.
- **No timeout meant no end.** One slow OCR call blocked a whole ingest. Each file now has a time budget, and progress
  prints `[n/total] name`. If a run seems stuck, read the progress, not the silence.
- **`verify` is exact and case-sensitive.** `$1250.00`, `1.250,00` and `total due` all return `present: false`
  against `Total due: $1,250.00`. Try the forms the document might use; do not loosen the match.
- **A wrong id is not an error.** `verify` against an id that does not exist returns `present: false`. Take the id from
  `find`.
- **`get` with no range returns the first 40 lines.** It looks like a range bug. Pass lines or `--pages`.
- **Summaries are not sources.** Gists and on-device summaries narrow the search; verify every value against the text.
- **Savings on a tiny corpus is negative.** The index has a fixed overhead (~2,000 tokens), so a one-file fixture
  shows a large negative saving. On a corpus of about 90 documents it measured 95% against images and 84% against
  full text.
- **The wrong Python.** A bare `python3` from an Xcode shell picked a different interpreter and packages. Pin the CLI
  to the project's virtualenv.

## What it does not cover

Whether the value means what Claude says it means (the operative reading of a clause, which of two dates governs),
values only in handwriting or images the OCR cannot read, and whether the document set itself is complete. A person
checks the meaning and the original page. For reducing screenshots of test results to text, see
[On-device image reduction](on-device-image-reduction.md).

## Loading this into Claude

> Documents here go through Dossier, not into context: `dossier ingest "<folder>" --work "<work>"`, then
> `dossier query "<work>" find "<text>"`, `get <id> <a> <b>` and `verify "<value>" <id>`. Quote a value only after
> `verify` returns `present: true`, in the document's own form. Before saying a document lacks something, check its
> `gap` rows and text length and find a word it is known to contain. Read every ingest summary, and treat
> `artifacts: 0` as a failure. On-device summaries narrow the search and are never the source.
