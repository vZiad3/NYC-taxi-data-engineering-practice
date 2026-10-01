# Notebook review

Reviewed all 49 cells in the attached `test1.ipynb`. The original file was left unchanged.

## Cleanup

- Removed 13 empty cells, the repeated passenger-count distribution, the repeated invalid-duration count, and the full-width vertical raw preview.
- Moved schema inspection next to the CSV read.
- Cleared all saved outputs and execution counts, including Spark progress logs and large tables.
- Added short section headings and kept simple Arabic notes alongside English labels.
- Centralized paths under `data/` and `output/`, relative to the project folder.
- Renamed the Spark app from `WebLogAnalysis` to `NYCTaxiPipeline`.
- Standardized `Average_speed` to `average_speed`, so later references also work with case-sensitive column resolution.
- Reused the raw row count and fixed a few printed labels. Investigation thresholds and calculations were preserved.

## Restored sections

The attachment only included Raw and Data Quality. Silver, SQL Analytics, Gold, and Zone Join were restored from the linked project conversation, where their code and results were available. These sections are additions to the attachment, not code that was already in it.

Preserved rules:

- Remove exact duplicates, then filter duration with `>= 0`; zero durations remain. This predicate also excludes null durations.
- Add the three zero-value flags and the financial mismatch flag with the original `0.01` tolerance and original six amount components.
- Retain original payment codes and add their names, pickup date, and pickup month.
- Keep records outside 2018, as decided later in the conversation. Recompute their count without filtering them out.
- Build summaries from the saved Silver and use the original left join to the zone lookup.
- Build Silver from raw data before writing, avoiding the prior read-and-overwrite dependency on the same Parquet folder.

Financial mismatch and zero-value flags are not null-validity checks: the original `otherwise(0)` behavior is preserved. Suspicious fares, speeds, distances, and passenger counts are retained. Gold does not filter on these flags. A monthly table is not guaranteed to have exactly 12 rows because the outside-2018 records remain.

## Validation

All Python cells were parsed for syntax, notebook structure was checked, and saved outputs, execution counts, and personal paths were checked. Full execution was not performed: the trip CSV and zone CSV are not available in this workspace. Historical counts are documented as historical, not fresh results. The runtime dependency versions were not present in the attachment, so no unverified version pins were added.
