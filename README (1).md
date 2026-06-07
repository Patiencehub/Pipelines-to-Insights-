# Food Delivery Analytics Dashboard
### Week 4 — Dash MVP | Data Engineering Pipelines | Spring 2026
**Student:** Njoroge, Patience

---

## Overview

An interactive analytics dashboard built with Plotly Dash, connected live to a PostgreSQL database populated by the Week 3 ETL pipeline. The dashboard surfaces operational insights from **15,000 food delivery orders** across three city tiers (Metro, Urban, Suburban).

---

## Screenshots

### Full Dashboard — KPI Cards & Charts
![Dashboard Overview](Pipelines_DASHBOARD_1.png)

### Delay Severity, Partner Efficiency & Order Volume
![Charts Row 2 and 3](Pipelines_DASHBOARD_2.png)

### Order Volume by Hour, Efficiency Histogram & City Tier Summary Table
![Summary Table](Pipelines_DASHBOARD_3.png)

---

## How to Run

### 1. Prerequisites
Make sure your Week 3 pipeline has been run and PostgreSQL is loaded with the `food_delivery` database.

### 2. Install dependencies
```bash
pip install dash dash-bootstrap-components plotly psycopg2-binary sqlalchemy pandas
```

### 3. Configure your database connection
Open `Week4_Dashboard.ipynb` and update Cell 3:
```python
DB_URL = "postgresql://postgres:YOUR_PASSWORD@localhost:5432/food_delivery"
```

### 4. Run the dashboard
Open `Week4_Dashboard.ipynb` in Jupyter and run all cells top to bottom.  
After Cell 8 starts, open your browser at: **http://127.0.0.1:8050**

---

## Dashboard Features

### Interactive Filters (Sidebar)
| Filter | Description |
|---|---|
| City Tier | Filter by Tier 1 Metro / Tier 2 Urban / Tier 3 Suburban |
| Customer Segment | Filter by Bronze / Silver / Gold / Platinum loyalty tier |
| Order Month | Filter by calendar month (January–December) |
| Hour Type | Toggle between all hours, peak (lunch 11–13 / dinner 18–21), or off-peak |

All four filters update all 6 charts and the KPI row simultaneously via Dash callbacks.

### KPI Cards
| Metric | Value (All Data) | Description |
|---|---|---|
| Total Orders | 15,000 | Filtered order count |
| Cancellation Rate | 13.4% | % of orders cancelled |
| On-Time Rate | 52.2% | % delivered on time or early |
| Avg Rev Margin | $96.66 | Net margin per order after fees and discounts |
| Total Revenue | $1.79M | Sum of final_amount_paid |
| Avg Efficiency | 59.2 | Mean delivery efficiency score |

### Visualizations

| Chart | Type | Business Insight |
|---|---|---|
| Cancellation Rate by City Tier | Bar chart | All three tiers show ~13% cancellation rate — problem is systemic, not geographic |
| Monthly Revenue Trend | Area line chart | Revenue is consistent across all 12 months (~$150K/month) |
| Delay Severity Distribution | Donut chart | 52.2% on time, 38.3% minor delay, 9.47% moderate delay |
| Partner Efficiency vs Experience | Line chart | Clear upward trend — efficiency rises from ~47 (1yr) to ~71 (15yrs) |
| Order Volume by Hour | Bar chart (peak highlighted in orange) | Demand is evenly distributed across all 24 hours |
| Efficiency Score by Tier | Histogram | All three city tiers show similar efficiency distributions centered around 50–70 |

### City Tier Summary Table (Live from PostgreSQL)
| City Tier | Orders | Cancel Rate | Avg Margin | Avg Rating | Promo Rate | On-Time Rate | Avg Efficiency |
|---|---|---|---|---|---|---|---|
| Tier 1 - Metro | 3,723 | 13.6% | $96.70 | 3.99 | 42.1% | 53.6% | 59.1 |
| Tier 2 - Urban | 3,757 | 13.5% | $96.17 | 3.99 | 41.8% | 52.4% | 59.4 |
| Tier 3 - Suburban | 7,520 | 13.2% | $96.88 | 4.0 | 42.6% | 51.5% | 59.1 |

---

## Business Insights

1. **Cancellation rates are uniform across city tiers** — all three tiers show ~13% cancellation, indicating the problem is systemic (preparation time, pricing, or demand forecasting) rather than location-specific.

2. **Partner experience directly drives efficiency** — the Partner Efficiency vs Experience chart shows a clear linear relationship, rising from ~47 at 1 year to ~71 at 15 years. High-value orders should be routed to experienced partners.

3. **On-time delivery needs improvement** — only 52.2% of orders arrive on time or early. The 38.3% minor delay rate suggests last-mile logistics optimization is needed.

4. **Revenue is stable year-round** — no seasonal spikes, indicating consistent demand across all months. Marketing campaigns should focus on increasing order value rather than volume.

5. **Promo code adoption is consistent** — ~42% across all tiers, suggesting promotions are not disproportionately driving cancellations or affecting margins significantly.

---

## Database Tables Used
| Table | Rows | Purpose |
|---|---|---|
| `fact_orders` | 15,000 | Order financials, customer attributes, engineered metrics |
| `fact_delivery_performance` | 15,000 | Delivery logistics and partner metrics |
| `dim_city_tier` | 3 | City tier reference lookup |
| `dim_order_time` | 1,727 | Time dimension (hour, day, month) |
| `city_tier_summary` | 3 | Pre-aggregated city KPIs |
| `partner_efficiency_summary` | 15 | Pre-aggregated partner metrics by experience year |

---

## Project Structure
```
├── Week4_Dashboard.ipynb                       # Dash dashboard (Jupyter)
├── Njoroge_Patience_Assignment_3_Fixed.ipynb   # Week 3 ETL pipeline
├── food_delivery_analytics_cleaned.csv         # Source dataset (15,000 rows)
├── analytics_exports/
│   ├── orders_analytics.csv
│   ├── delivery_performance_analytics.csv
│   ├── city_tier_summary.csv
│   └── partner_efficiency_summary.csv
├── logs/
│   └── pipeline_week3.log
├── Pipelines_DASHBOARD_1.png                   # Screenshot 1 — KPI cards
├── Pipelines_DASHBOARD_2.png                   # Screenshot 2 — Charts row 2 & 3
├── Pipelines_DASHBOARD_3.png                   # Screenshot 3 — Summary table
└── README.md
```

---

## Dependencies
```
dash>=2.14.0
dash-bootstrap-components>=2.0.0
plotly>=5.18.0
psycopg2-binary>=2.9.9
sqlalchemy>=2.0.0
pandas>=2.0.0
numpy>=1.24.0
```
