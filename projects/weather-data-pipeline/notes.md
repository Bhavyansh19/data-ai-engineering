# Weather Data Pipeline Notes

I used this project to understand how a basic ingestion pipeline works. I’m not treating it as a serious resume project right now.

The flow is:

```text
run tests → call API → save raw JSON → validate and transform → save processed JSON → append CSV → save SQLite → analyze
```

For now, I’m keeping the project paused and using it mainly to learn from.
