# 2026-10-16

## TransitFlow

- Added a PostgreSQL table for historical realtime trip updates.
- Added an incremental loader from content-hashed JSON snapshots into PostgreSQL.
- Used `(snapshot_hash, entity_id)` as the primary key for conflict-safe reruns.
- Used `ON CONFLICT DO NOTHING` so already-loaded snapshot entities are skipped.
- Kept database connection settings configurable through `PGHOST`, `PGPORT`, `PGDATABASE`, `PGUSER`, and `PGPASSWORD`.
