# EDA with SQL — Job Market Analysis

This was my first proper SQL analysis project. I used job posting data to look at what skills are being asked for in data engineering jobs, which skills seem to be connected with higher salaries, and which ones might be worth learning first.

I was mainly trying to answer three questions:

- What are the most demanded skills for data engineers?
- Which skills have the highest salaries?
- Which skills have a good balance between demand and salary?

## What I worked with

The data was organized into a few related tables:

- `job_postings_fact` — information about the job postings
- `skills_dim` — the list of skills
- `skills_job_dim` — the table connecting jobs and skills

The `skills_job_dim` table was important because one job can need multiple skills, and one skill can appear in many jobs. I had to join these tables together before I could group the results by skill.

## What I learned

While working on this, I learned:

- The basics of DuckDB and how to use it to run analytical SQL locally.
- The basics of MotherDuck and how it can be used with DuckDB databases in a cloud environment.
- How fact, dimension, and bridge tables fit together in a simple data warehouse.
- How to join multiple tables to answer a real question instead of just querying one table.
- How `COUNT()` can be used to measure how often a skill appears in job postings.
- How `MEDIAN()` is useful for salary analysis because one unusually high or low salary does not affect it as much as an average would.
- How to filter the data using conditions like data engineer roles, remote jobs, and available salary information.
- The difference between filtering rows with `WHERE` and filtering grouped results with `HAVING`.
- How to sort and limit results to find the top skills.
- How to create new calculated columns using functions like `ROUND()` and `LN()`.
- Why looking only at salary can be misleading. A skill may have a high salary but show up in very few jobs.
- Why SQL and Python are still the most practical skills to focus on first based on the results.
- How to save my SQL work in Git and keep it organized as part of my learning journey.

## The queries

### `01_top_demanded_skills.sql`

This finds the ten skills that appear most often in remote data engineer job postings. SQL and Python came out at the top, followed by AWS, Azure, Spark, Airflow, and other common tools.

### `02_top_paying_skills.sql`

This looks at the median salary for each skill. I also included the number of job postings so I could see whether a skill was actually common or just appeared in a small number of highly paid jobs.

### `03_optimal_skills.sql`

This was my attempt to combine demand and salary into one score. I used the natural log of the demand count so that extremely common skills did not completely overpower the salary part of the calculation.

## Things I noticed

SQL and Python showed up the most, which confirmed that they are the foundation for data engineering. AWS and Azure were also very common. Spark, Airflow, Snowflake, Databricks, and Kafka came up often too.

Some infrastructure skills, especially Terraform and Kubernetes, showed strong salary results. But I also noticed that the highest-paying skill is not automatically the best skill to learn first. Demand matters as well, which is why the final query was useful.

These results are just for learning and depend on the dataset and filters I used. They are not meant to be a perfect picture of the entire job market.

## Files

- [`01_top_demanded_skills.sql`](./01_top_demanded_skills.sql)
- [`02_top_paying_skills.sql`](./02_top_paying_skills.sql)
- [`03_optimal_skills.sql`](./03_optimal_skills.sql)

The queries were written for DuckDB. I included the output in the SQL files so I can look back at what I found without having to rerun everything immediately.
