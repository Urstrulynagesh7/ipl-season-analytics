# IPL Season Analytics Dashboard

A end-to-end data analytics project on IPL match and ball-by-ball data — from raw CSVs to SQL analysis to an interactive Power BI dashboard.

## Overview

This project analyzes a season of IPL (Indian Premier League) cricket data to answer questions about player performance, team strength, and venue characteristics. It covers the full analytics workflow: data cleaning in Python, querying with SQL, and visualization in Power BI.

## Questions Explored

- Who were the top run-scorers of the season?
- Which batters had the best strike rates (minimum 30 balls faced)?
- Which teams had the highest win percentage?
- Which venues produced the highest average first-innings scores?
- Who took the most wickets?

## Dataset

- `matches.csv` — 39 matches: teams, venue, toss, result, and match-level stats
- `deliveries.csv` — 17,477 ball-by-ball records: batter, bowler, runs, wicket details

Source: Kaggle IPL dataset (season-level match and delivery data).

## Approach

1. **Data exploration (Python / pandas)** — Loaded both CSVs, checked structure, and investigated missing values. Found that missing `wb_runs`/`wb_wickets` fields were expected (super-over stats, only populated for tied matches), and one match (KKR vs PBKS) had a no-result outcome after the toss, likely due to rain.
2. **SQL analysis (SQLite)** — Loaded the cleaned data into a local SQLite database and wrote queries for top scorers, strike rates, team win percentage, venue-wise scoring, and top wicket-takers. Along the way, debugged a silent filtering bug: the `wide` column used `0` rather than `NULL` for non-wide deliveries, which had been silently zeroing out a strike-rate query — a good reminder to verify assumptions about how missing/zero values are encoded before trusting a filter.
3. **Dashboard (Power BI)** — Imported the query results and built a 4-panel dashboard with sorted bar charts for each metric, using a consistent color theme.

## Dashboard

![IPL Season Analytics Dashboard](dashboard_screenshot.png)

## Key Insights

- Vaibhav Sooryavanshi led the season in both total runs and strike rate — a rare combination of volume and explosiveness.
- PBKS had the highest win percentage among all teams this season.
- Sawai Mansingh Stadium, Jaipur produced the highest average first-innings scores, suggesting a batting-friendly pitch.

## Tools Used

Python (pandas), SQL (SQLite), Power BI

## Files in this repo

- `ipl_analysis.ipynb` — data exploration and cleaning
- `queries.sql` — all SQL queries used
- `*.csv` — exported query results (data source for the dashboard)
- `ipl_dashboard.pbix` — Power BI dashboard file
- `dashboard_screenshot.png` — static preview of the dashboard
