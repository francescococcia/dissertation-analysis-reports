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

## Notes

- Reports are tied to an exact plugin + framework version (recorded in each
  `.txt` header), so a result can always be traced to the code that produced it.
- Memory captures themselves (`.core` / `.raw` / `.dmp`) are **not** stored here —
  they are large and kept outside version control.
- Newer runs write to `~/analysis-reports` (the framework's default `REPORT_DIR`).
