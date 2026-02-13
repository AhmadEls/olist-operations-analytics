# Olist Operations Analytics — Delivery SLA Dashboard

## Project Overview

This project analyzes delivery performance and Service Level Agreement (SLA) compliance using the Olist e-commerce dataset. The objective is to evaluate fulfillment efficiency, delivery reliability, and operational performance through a structured business intelligence workflow and executive-level dashboard.

The solution is built using a layered data modeling approach, where raw transactional data is transformed into aggregated SLA metrics and presented through a clean reporting layer in Power BI.

---

## Business Context

In e-commerce operations, delivery reliability directly impacts customer satisfaction, retention, and brand trust. Missed delivery promises can increase support costs, reduce seller credibility, and damage platform reputation.

This project addresses the need for structured SLA monitoring by providing visibility into:

- Overall delivery volume
- On-time delivery performance
- Late shipment frequency
- Severity of SLA breaches (average days late)
- Performance variations across regions and sellers

The dashboard is designed to support operational monitoring and performance evaluation at both executive and operational levels.

---

## Key KPIs

- **Delivered Orders** — Total successfully completed deliveries  
- **On-Time Orders** — Deliveries completed on or before the estimated date  
- **Late Orders** — Deliveries completed after the estimated date  
- **On-Time Rate (%)** — On-Time Orders ÷ Delivered Orders  
- **Average Days Late** — Average delay duration for late deliveries  

All KPIs are engineered in SQL prior to visualization to ensure clear metric definitions and consistent aggregation logic.

---

## Methodology

The project follows a structured BI architecture:

1. Raw data ingestion into SQLite  
2. SQL-based data cleaning and staging  
3. Aggregated SLA metric layer creation  
4. Semantic modeling in Power BI  
5. Executive dashboard reporting  

This separation of raw, staging, and metric layers ensures:

- Clear grain definition  
- Controlled aggregation logic  
- Query performance efficiency  
- Scalable reporting structure  

---

## Key Insights (Preliminary)

Based on the engineered SLA metrics:

- Approximately 91–92% of deliveries meet the promised delivery date.
- Nearly 8% of deliveries are late, indicating operational friction in fulfillment or logistics.
- Late deliveries average around 9–10 days beyond the estimated delivery date, suggesting that delays are not minor deviations but significant SLA breaches.
- Monitoring seller-level and regional performance is critical to identifying systemic vs localized issues.

These findings highlight the importance of SLA tracking in maintaining customer satisfaction and operational efficiency.

---

## Assumptions & Limitations

- SLA performance is calculated only for orders marked as "delivered".
- Late severity (average days late) considers only delayed deliveries.
- Estimated delivery date is treated as the official SLA commitment.
- This analysis does not account for shipment carrier performance, warehouse processing delays, or customer availability factors.
- Data reflects historical transactional records and may not represent real-time operational performance.

These constraints should be considered when interpreting SLA metrics.

---

## Tools & Technologies

### Data Storage & Modeling
- **SQLite** — relational database for structured data storage  
- **SQL** — data transformation, staging logic, and SLA metric computation  

### Business Intelligence
- **Power BI Desktop** — semantic modeling and executive dashboard development  

### Version Control
- **Git** — version control and project tracking  
- **GitHub** — repository hosting and documentation  

---

## Repository Structure

```
olist-operations-analytics/
│
├── data/                # Raw dataset
├── database/            # SQLite database file
├── sql/                 # SQL scripts for staging and metrics
├── docs/                # Documentation (data model, KPI definitions)
├── BUSINESS_BRIEF.md    # Business context and analysis framing
└── README.md            # Project overview
```

---

## Project Positioning

This project demonstrates:

- SQL-based metric engineering  
- Dimensional modeling principles  
- SLA performance analysis  
- Executive KPI dashboard design  
- Structured BI project workflow  

It is positioned as both a **Data Analyst** and **BI Developer** portfolio project, showcasing end-to-end analytics from raw data modeling to executive reporting.

