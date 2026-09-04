# Dissertation Analysis Reports

Generated memory-forensics analysis reports for the dissertation
**detection framework** (Coccia, F., 2026) — the raw evidence produced by
`analyze_capture.sh` across the project's technique runs.

These are **outputs, not code**. The framework that generates them lives in
[`dissertation-detection-framework`](https://github.com/francescococcia/dissertation-detection-framework);
the narrative documentation lives in the `dissertation-vault`. This repo is the
versioned archive of the reports themselves, kept so results are reproducible and
citable.

## What's here

Each analysis run produces a timestamped set (`report-YYYYMMDD-HHMMSS.*`):

| Extension | Content |
|-----------|---------|
| `.txt` | Full multi-plugin text report (windows.info, pslist, pstree, cmdline, malfind, ldrmodules, reflective_load, SUMMARY, SCAN SUMMARY) |
| `.csv` | Raw `reflective_load` detection rows (Volatility `-r csv`) |
| `.html` | Styled card report of the `reflective_load` result |
| `-full.html` | Collapsible full multi-plugin HTML report |
| `-ioc.json` | Structured IOC feed for SIEM ingestion (runs with detections only) |

## Coverage

56 runs, **2026-08-09 – 2026-09-03**, against these captures:

| Capture | Runs | Technique / purpose |
|---------|-----:|---------------------|
| `T1620-poc-capture.core` | 14 | Reflective load PoC |
| `T1620-4-exclusion-free.core` | 10 | Reflective load, exclusions disabled |
| `FP-check-expanded.core` / `FP-check-capture.core` | 7 | False-positive baseline |
| `T1055-12-*.core` / `Dll-inject-*.core` | 7 | Process hollowing / DLL injection |
| `blackenergy.raw` / `Challenge.raw` | 5 | Public reference samples |
| `T1620-native-rw-*.core` / `T1620-native-rwx-*.core` | 5 | Native RW vs RWX allocation variants |
| `T1218.010-1-run2-capture.core` | 3 | Regsvr32 proxy execution |
| `FP-win10-*.core` | 2 | False-positive baseline (Windows **Server 2022**; filename is misleading) |
| `T1546-003-1-run2-capture.core` | 2 | WMI event subscription |
| `T1620-3-capture.core` | 1 | Reflective load variant |

Runs from `20260824-233039` onward carry a `Plugin:`/`Framework:` header line in
the `.txt` (ReflectiveLoad v1.3.0, then v1.4.0 from `20260825-175831`); earlier
runs record the framework version only, inside each plugin section. The
`20260903` runs are the specificity result (0 false positives on the `FP-win10`
Server 2022 baseline) and its re-run.

## Notes

- Reports are tied to an exact plugin + framework version (see Coverage above),
  so a result can always be traced to the code that produced it.
- Memory captures themselves (`.core` / `.raw` / `.dmp`) are **not** stored here —
  they are large and kept outside version control.
- `malfind-FP-check-expanded-20260904.txt` is a standalone `windows.malfind` dump
  of the benign Server 2022 baseline — the reproducible source for the "22 false
  positives vs. 0" specificity evidence (malfind alone flags 22 benign JIT/AV regions;
  the combined `reflective_load` gate flags 0).
- Runs are generated wherever `analyze_capture.sh` is invoked (the framework's
  default `REPORT_DIR`, or the Volatility 3 working directory) and archived into
  this repo afterwards.
