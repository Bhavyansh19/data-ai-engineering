# TransitFlow

TransitFlow is my main Data Engineering project using real BART transit data.

## What works right now

The local MVP can:

- download the BART static GTFS ZIP when raw files are missing
- load the GTFS `.txt` files with pandas
- check that important files and columns exist
- check that table IDs connect correctly
- check for missing and duplicate keys
- join trips, routes, stop times, and stops
- write a detailed schedule file
- write a route-level summary file
- run automated tests

## Current flow

```text
BART GTFS ZIP
→ data/raw/gtfs_static/
→ pandas tables
→ validation
→ joins
→ data/processed/scheduled_stop_events.csv
→ data/processed/route_schedule_summary.csv
```

## Main files

- `src/run_pipeline.py` — runs the local pipeline
- `src/ingest_static_gtfs.py` — downloads, loads, validates, and joins data
- `tests/` — automated checks

## How to run

```bash
source .venv/bin/activate
python src/run_pipeline.py
python -m pytest -q
```

## What I learned

- GTFS has related tables, not one giant CSV.
- `stop_times` is one row per trip at one stop.
- `trip_id + stop_sequence` identifies a stop event.
- pandas `merge()` is similar to a SQL join.
- `size()` counts rows and `nunique()` counts distinct values.
- Raw data and processed data should be kept separately.
- Validation catches missing files, columns, relationships, and duplicate keys.

## Next

Understand the local MVP first. Then add a database, dbt, AWS, and Airflow one at a time.
