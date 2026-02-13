# Interview Summary — Olist Delivery SLA Dashboard

## Project Summary

This project analyzes delivery performance using the Olist e-commerce dataset.  
The goal was to evaluate SLA compliance and delivery reliability using a structured SQL-first BI approach.

## What I Built

- Designed a layered data pipeline (raw → staging → metric layer)
- Engineered SLA metrics in SQL
- Built aggregated executive KPI tables
- Created a Power BI dashboard for SLA monitoring
- Structured the project using Git and documented the full workflow

## Key Technical Decisions

- Pre-aggregated metrics in SQL instead of calculating everything in Power BI
- Separated staging and reporting layers for clarity and performance
- Avoided metric-to-metric relationships in the BI model
- Designed KPIs for executive consumption

## Business Impact

The dashboard enables:
- Monitoring on-time delivery performance
- Identifying SLA breach severity
- Comparing seller and regional performance
- Supporting operational improvement discussions

## What I Would Improve Next

- Add dynamic month-over-month comparison
- Implement SLA target benchmarking
- Introduce DAX measures for flexible filtering
- Add trend and variance visuals
