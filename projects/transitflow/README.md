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
- load the local star schema into PostgreSQL
- build staging views and mart tables with dbt
- build a route-level summary mart with event, trip, and stop counts
- land identical realtime feed contents only once during reruns
- load realtime snapshots incrementally into PostgreSQL without duplicate rows
- expose realtime PostgreSQL records through a dbt staging view
- fetch real BART departure estimates through the official ETD API with a 403 fallback
- load ETD snapshots into PostgreSQL and expose an analytics-ready realtime departures mart
- run dbt tests for nulls, duplicates, composite keys, and relationships

## Current flow

```text
BART GTFS ZIP
→ data/raw/gtfs_static/
→ pandas tables
→ validation
→ joins
→ data/processed/scheduled_stop_events.csv
→ data/processed/route_schedule_summary.csv
→ PostgreSQL transitflow database
→ dbt source definitions
→ staging views
→ analytics mart tables, including realtime departures
```

## Main files

- `src/run_pipeline.py` — runs the local pipeline
- `src/ingest_static_gtfs.py` — downloads, loads, validates, and joins data
- `tests/` — automated checks
- `sql/warehouse_schema.sql` — PostgreSQL tables and constraints
- `dbt/` — dbt project, staging models, mart models, and tests
- `src/ingest_bart_etd.py` — live BART departure ingestion
- `src/load_bart_etd_to_postgres.py` — incremental ETD warehouse loader

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
- A star schema separates event data in a fact table from descriptive data in dimensions.
- PostgreSQL can enforce primary-key and foreign-key rules while loading data.
- `source()` points to an existing warehouse table; `ref()` points to another dbt model.
- Staging models are usually views, while mart models are persistent tables.
- dbt can build models and test data quality with one `dbt build` command.
- `GROUP BY` and `COUNT(DISTINCT ...)` can turn fact events into route-level metrics.
- Content-hashed raw filenames make realtime snapshot landing idempotent.
- The realtime warehouse loader uses `(snapshot_hash, entity_id)` with `ON CONFLICT DO NOTHING`.
- Realtime records are now registered as a dbt source and tested in staging.
- Updated the trip-update endpoint to BART's newer platform-based feed; terminal access remains
  dependent on Cloudflare verification.
- Added a working ETD JSON path for local demos. It tries BART's official endpoint first and uses
  a read-only relay only after a Cloudflare 403. The API can return zero departures outside BART
  operating hours; that is a real empty response, not generated sample data.

## Next

The local PostgreSQL warehouse, dbt layer, and realtime ETD path are now working. Next, understand
the new ETD files and then move to AWS or Airflow.
