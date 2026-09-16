# Exploratory Data Analysis with SQL: Data Engineer Job Market

This project uses SQL to explore the data engineer job market through job-posting data. The goal was to move from broad career questions—what employers ask for, which skills are associated with higher pay, and what is worth learning—to repeatable analytical queries.

## Questions answered

1. Which skills appear most often in remote data engineer job postings?
2. Which skills have the highest median annual salary among skills with meaningful demand?
3. Which skills offer a practical balance of demand and compensation?

## What I learned

- How a star-schema style warehouse supports analysis: a job-postings fact table is connected to skill and job-skill bridge tables.
- How to solve many-to-many relationships by joining a bridge table before grouping by skill.
- How to write analytical SQL with `INNER JOIN`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, and `LIMIT`.
- How to use `COUNT` to measure skill demand and `MEDIAN` to make salary comparisons less sensitive to extreme values.
- Why incomplete salary records should be excluded when the analysis depends on compensation.
- How filters such as job title, remote status, and salary availability change the population being analyzed.
- How to create derived metrics with `ROUND` and `LN` for easier comparison and ranking.
- Why demand and salary should be considered together: a rare, high-paying skill is not automatically the best first skill to learn.
- How to keep query output readable and explain the business purpose of each analysis.
- The basics of DuckDB for running fast, local analytical SQL queries and the basics of MotherDuck for working with DuckDB databases in a cloud-connected environment.
- How Git helps organize, review, and publish SQL learning projects.

## Query guide

| File | Purpose |
| --- | --- |
| [`01_top_demanded_skills.sql`](./01_top_demanded_skills.sql) | Finds the ten most frequently requested skills for remote data engineer roles. |
| [`02_top_paying_skills.sql`](./02_top_paying_skills.sql) | Ranks skills by median annual salary while retaining demand counts. |
| [`03_optimal_skills.sql`](./03_optimal_skills.sql) | Combines log-transformed demand and median salary into an exploratory skill score. |

## Main findings

The results show that SQL and Python are foundational skills, followed by major cloud platforms such as AWS and Azure. Spark, Airflow, Snowflake, and Databricks also appear frequently in remote data engineering roles. Infrastructure skills such as Terraform and Kubernetes rank strongly in the salary-oriented analysis, while the combined score highlights skills that are both useful in the market and valuable enough to prioritize.

These findings are directional rather than universal salary guidance: they depend on the source data, the remote-job filter, the salary fields available, and the minimum-demand threshold used in each query.

## Data model used

- `job_postings_fact` — job titles, work location, salary, and posting details
- `skills_job_dim` — bridge table connecting jobs to skills
- `skills_dim` — skill names and metadata

The queries are written for DuckDB and use DuckDB-compatible analytical functions such as `MEDIAN`. This project also introduced the basics of MotherDuck, including how it can provide a hosted environment for accessing and analyzing DuckDB data.

## How to review

Open the SQL files in order. Each file includes the business question, query logic, and a sample result captured from the analysis. To run them against a compatible database, make sure the three tables above are available in the current DuckDB session.
