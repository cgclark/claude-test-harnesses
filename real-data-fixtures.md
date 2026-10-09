# Real-data fixtures

> Lets Claude test an algorithm against a thinned copy of the user's real recorded data, with assertions labelled by the user, so it can see failures that tidy synthetic inputs never produce.

**Applies to:** any heuristic over messy recorded data: GPS track clustering and matching, sensor or health
series, logs, OCR output · **Needs:** read access to an export of the real corpus, a script to thin it, a test
target that can bundle resource files (XCTest via XcodeGen/Xcode here; any runner works)

## Why it exists

By default Claude generates synthetic inputs (perfect circles, clean series), writes tests against them, and
reports green. Real data has GPS scatter, altitude noise, a watch that auto-starts late, detours, dead batteries
and a second recording of the same ride.

Built for route clustering in a cycling app. It passed 174 synthetic tests while splitting one real 65 km loop,
ridden many times, into four routes. Two bugs showed up only on real tracks:

- The corridor test used **mean** distance to the reference road. One detour wrecks a mean (487 m mean against
  12 m median). It now uses the **fraction** of the ride within 120 m of the road.
- Ride direction came from speed versus gradient on **GPS altitude**. That signal is noise, and it was
  intransitive. It is now used only when real terrain data exists; map progress decides otherwise.

## What it does

1. Export the real corpus from where the app gets it (here, GPX files from a health-data export).
2. Thin and convert it into one JSON fixture checked into the test target.
3. Load the fixture in a test and run it through **the same normalization the app applies on ingest**, then
   through the code under test.
4. One test **prints the evidence** (the measured terms behind every verdict) for every pair. It asserts
   nothing; it is there to be read.
5. Other tests assert the outcomes the user confirmed (ride X belongs to route Y, ride Z is its own route), and
   each failure message names the case.

## Recipe

**1. Thin the corpus** into a fixture. Spacing of roughly 40 m keeps road shape and keeps the file to a few MB:

```python
#!/usr/bin/env python3
# thin.py <out.json> <track.gpx>...  ->  {stem: [{lat, lon, ele, t}]}, t = seconds from first point
import json, math, sys, xml.etree.ElementTree as ET
from datetime import datetime
from pathlib import Path
SPACING = 40.0
def metres(a, b):
    la1, lo1, la2, lo2 = map(math.radians, (a[0], a[1], b[0], b[1]))
    h = math.sin((la2-la1)/2)**2 + math.cos(la1)*math.cos(la2)*math.sin((lo2-lo1)/2)**2
    return 2 * 6_371_000 * math.asin(math.sqrt(h))
def track(path):
    pts = []
    for el in ET.parse(path).getroot().iter():
        if el.tag.endswith("trkpt"):
            ele = next((c.text for c in el if c.tag.endswith("ele")), "0")
            tm = next((c.text for c in el if c.tag.endswith("time")), None)
            t = datetime.fromisoformat(tm.replace("Z", "+00:00")).timestamp() if tm else 0.0
            pts.append((float(el.get("lat")), float(el.get("lon")), float(ele), t))
    kept = pts[:1]
    for p in pts[1:]:
        if metres(kept[-1], p) >= SPACING: kept.append(p)
    if pts and kept[-1] != pts[-1]: kept.append(pts[-1])   # keep the true finish
    t0 = kept[0][3] if kept else 0
    return [{"lat": round(a, 6), "lon": round(o, 6), "ele": round(e, 1), "t": round(t - t0, 1)}
            for a, o, e, t in kept]
out = {Path(p).stem: track(p) for p in sys.argv[2:]}
json.dump(out, open(sys.argv[1], "w"))
print(f"{len(out)} tracks -> {sys.argv[1]}")
```

```bash
python3 thin.py <Tests>/Fixtures/<corpus>.json <export-dir>/route_*.gpx
```

**2. Bundle the fixture** with the test target. XcodeGen `project.yml`:

```yaml
<App>Tests:
  sources:
    - path: Tests
  resources:
    - path: Tests/Fixtures
```

**3. Load it through the real pipeline:**

```swift
let url = try XCTUnwrap(Bundle(for: Self.self).url(forResource: "<corpus>", withExtension: "json"),
                        "fixture missing from the test bundle")
let raw = try JSONDecoder().decode([String: [Point]].self, from: Data(contentsOf: url))
// Build the app's own fix type, then normalise exactly as ingest does. Raw points are not the device pipeline.
let reference = <Reference>(id: key, fixes: <Normaliser>.normalise(fixes))
```

**4. Split measurement from judgement** in the code under test: `evidence(a, b) -> Evidence` returns every
term (length ratio, on-road fraction, median and worst corridor distance, coverage, direction...), and
`judge(Evidence) -> Bool` applies the thresholds. Give `Evidence` a one-line `summary`.

**5. Add a report test** that prints `summary` and the verdict for every pair, and a sanity test that the fixture
is still the history you think it is (count, how many of the dominant case).

**6. Set thresholds from the gap in the data.** Read the printed evidence and put the threshold in the gap
between the groups. In the cycling app, same-loop rides scored on-road 0.78–1.00 and a different route 0.47, so the
threshold went to 0.70. Do not tune from intuition.

**7. Assert the user's labels**, grouped by kind (complete, interrupted, detour, its-own-route), with the reason
in a comment. Ask the user to confirm the labels; do not infer them from the algorithm's own output.

```bash
xcodebuild test -project <App>.xcodeproj -scheme <scheme> \
  -destination 'platform=iOS Simulator,name=<device>' -only-testing:<App>Tests/<RealDataTests>
```

## Traps

- **Seeded test data becomes real data.** A debug seeder wrote synthetic rides into the shared health store so the
  simulator had something to show. Once saved they were ordinary workouts: on a device they formed a fake route in
  the picker, added to training load, were synced as history, and drew as a perfect ellipse. Claude spent several
  rounds defending that ellipse as the user's real route. Fix: filter app-written records out of the library by
  source (`sourceRevision.source.bundleIdentifier == Bundle.main.bundleIdentifier`), mark records the app records
  for real with a metadata key so the filter keeps them, and purge seeded records on launch. HealthKit only lets
  an app delete what it wrote, so the purge cannot touch real data. Gate both to device builds; on a simulator the
  seeder is the only data. When output looks wrong, check where the input came from before blaming the renderer.
- **Skipping normalization.** Feeding raw points to the clusterer tests a pipeline the device never runs.
- **Means over messy data.** One outlier destroys a mean. Use fractions within a tolerance, or medians.
- **Derived signals from noisy channels.** GPS altitude is not good enough for gradient. Use it only when a
  better source exists, and model "no opinion" as nil rather than as disagreement.
- **A single threshold for several relationships.** Same/different was not enough. The data had four cases:
  complete, interrupted (flat battery, finishes far from its own start), detour (same length/start/direction,
  only about half within the corridor because a grid city diverts onto a parallel street), and a deliberate shorter
  loop that returns home. Each needed its own rule and its own handling in statistics.
- **Hypotheses that look right on intuition.** Two were refuted by the printed evidence. Coverage span: a 60%
  prefix of a loop read 0.98, because the return leg runs near the outbound. A "comes home" test had been checked
  against a wrongly labelled set. Measure first.
- **Asymmetric comparisons.** `same(a, b) != same(b, a)` made membership depend on comparison order. Always
  measure in the frame of the longer item.
- **Caches hide fixes.** If grouping is cached, bump the cache version whenever a rule change would regroup the same
  data, or the device keeps serving the old answer and the fix looks like a no-op.
- **Privacy of the fixture.** Real tracks start and end at the user's home and carry real timestamps. Keep the
  fixture in a private repo, or transform it before committing it anywhere public: shift every coordinate by a
  constant offset and rebase times to an arbitrary epoch, so geometry is preserved and location is not.

## What it does not cover

Data the corpus does not yet contain (a route never ridden, another rider's habits), live ingestion timing on the
device, sync between devices, and whether the user agrees with a label. The human still confirms each label and
checks the result on the phone.

## Loading this into Claude

> Algorithms over recorded data are tested against `<Tests>/Fixtures/<corpus>.json`, a thinned copy of real
> recordings, loaded through the app's own normaliser. Before changing a threshold, run the evidence report
> (`-only-testing:<App>Tests/<RealDataTests>/testReportEvidence`) and set it from the gap in the printed
> measurements. Synthetic tests are additions, never the proof. Never let seeded or test records into a store the
> app reads as real, and bump the cache version when a rule change would regroup existing data.
