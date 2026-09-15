# Swiggy Restaurant Data Analysis

An end-to-end data analysis and visualization project that explores Swiggy's restaurant listings across **9 major Indian cities** and presents the findings through an interactive **Power BI** dashboard.

The project walks through the full analytics workflow — from raw CSV ingestion and data cleaning in Power Query, to DAX-based feature engineering, and finally to a multi-page report designed for quick business insights on pricing, ratings, delivery performance, and cuisine distribution.

---

## Table of Contents

- [Overview](#overview)
- [Live Dashboard Preview](#live-dashboard-preview)
- [Dataset](#dataset)
- [Repository Structure](#repository-structure)
- [Key Insights Uncovered](#key-insights-uncovered)
- [Power BI Report Walkthrough](#power-bi-report-walkthrough)
- [Getting Started](#getting-started)
- [Technologies Used](#technologies-used)
- [Data Source & Attribution](#data-source--attribution)
- [Future Enhancements](#future-enhancements)

---

## Overview

Swiggy is one of India's largest food-delivery platforms. This project takes a publicly available Swiggy restaurant-dataset (8,680 records across 9 cities) and turns it into an executive-ready Power BI report answering questions such as:

- Which cities have the most affordable vs. premium restaurant landscape?
- Where do customers leave the highest ratings, and is rating volume concentrated in a few chains or spread out?
- How does delivery time correlate with price, rating, or city?
- Which cuisines dominate each market, and which are niche?

The report is built to be consumed by non-technical stakeholders — every page tells a story, with KPIs on top and supporting visuals below.

---

## Live Dashboard Preview

> Open `Swiggy Data Analysis.pbix` in Power BI Desktop to interact with the report. A static snapshot of the summary page is shown below.

| Page | Focus |
|------|-------|
| **Summary Overview** | KPI cards (Total Restaurants, Avg Price, Avg Rating, Avg Delivery Time) + city-wise breakdown |
| **City Analysis** | City slicer with rating distribution, price bucket, and top areas |
| **Cuisine Insights** | Cuisine frequency, top-rated cuisines, cuisine vs. price heatmap |
| **Delivery Performance** | Delivery time by city, price tier vs. delivery time scatter |

---

## Dataset

The raw dataset (`swiggy.csv`) contains **8,680 restaurant records** across **9 Indian cities** and **10 columns**.

### Schema

| Column | Type | Description |
|--------|------|-------------|
| `ID` | Integer | Unique Swiggy restaurant identifier |
| `Area` | String | Locality / neighborhood within the city |
| `City` | String | One of 9 cities: Bangalore, Hyderabad, Mumbai, Pune, Kolkata, Delhi, Chennai, Ahmedabad, Surat |
| `Restaurant` | String | Restaurant display name |
| `Price` | Float | Average price for two (INR). Range: 0 – 2,500 |
| `Avg ratings` | Float | Average customer rating. Range: 2.0 – 5.0 |
| `Total ratings` | Integer | Number of customer ratings received |
| `Food type` | String | Pipe/comma-separated cuisine tags (e.g., `Biryani,Chinese,North Indian`) |
| `Address` | String | Street / area-level address |
| `Delivery time` | Integer | Estimated delivery time in minutes. Range: 20 – 109 |

### Quick Stats

| Metric | Value |
|--------|-------|
| Total restaurants | 8,680 |
| Cities covered | 9 |
| Unique cuisine tags | ~600 |
| Average price (for two) | ₹348.44 |
| Average rating | 3.66 / 5.0 |
| Average delivery time | ~54 minutes |
| Largest city (by records) | Kolkata (1,346) |
| Smallest city (by records) | Surat (512) |

---

## Repository Structure

```
Swiggy-Restaurant-Data-Analysis/
│
├── Swiggy Data Analysis.pbix    # Power BI report file (open with Power BI Desktop)
├── swiggy.csv                   # Raw dataset (8,680 rows × 10 columns)
├── README.md                    # This file
└── LICENSE                      # MIT License
```

---

## Key Insights Uncovered

A few of the headline insights surfaced by the dashboard:

1. **Kolkata leads in restaurant density** with 1,346 listings — nearly 2.6× the size of Surat (512), making it the most competitive Swiggy market in this dataset.
2. **Pricing is highly city-dependent.** Average price for two ranges across cities, with metros like Mumbai and Bangalore skewing toward the higher end, while Ahmedabad and Surat trend more affordable.
3. **Ratings cluster around 3.6–3.7** on average — Swiggy users are moderate graders. Very few restaurants cross the 4.5 mark, and those that do tend to be premium or single-cuisine specialists.
4. **Delivery time is weakly correlated with price** — expensive restaurants are not consistently faster. The 50–60 minute band is the most common delivery window across all cities.
5. **North Indian, Chinese, and Biryani dominate the cuisine mix**, but each city has a distinctive long tail — e.g., Kolkata shows stronger Mughlai/Lucknowi representation, while Chennai shows more South Indian variety.

> These insights are illustrative — open the `.pbix` file to drill down and verify each claim interactively.

---

## Power BI Report Walkthrough

### Data Preparation (Power Query)
- Removed rows with null/zero `Price` and `Avg ratings`.
- Trimmed and title-cased `City`, `Area`, and `Restaurant` columns.
- Split the comma-separated `Food type` column into a cuisine lookup table for many-to-many analysis.
- Created a `Price Tier` column: *Budget (<₹300) / Mid (₹300–₹600) / Premium (₹600–₹1000) / Luxury (>₹1000)*.
- Created a `Delivery Speed` column: *Fast (<35 min) / Standard (35–60 min) / Slow (>60 min)*.

### DAX Measures
- `Total Restaurants = COUNTROWS(Restaurants)`
- `Avg Price = AVERAGE(Restaurants[Price])`
- `Avg Rating = AVERAGE(Restaurants[Avg ratings])`
- `Avg Delivery Time = AVERAGE(Restaurants[Delivery time])`
- `Rating Volume = SUM(Restaurants[Total ratings])`
- `Top 5 Cities by Restaurant Count = TOPN(5, SUMMARIZE(...))`

### Visuals by Page
- **Summary Overview** — 4 KPI cards, bar chart of restaurants per city, donut chart of price tiers.
- **City Analysis** — Matrix of city × metric, slicer for city, top-10 areas bar chart.
- **Cuisine Insights** — Word cloud of cuisines, top-10 highest-rated cuisines, stacked bar of cuisine per city.
- **Delivery Performance** — Scatter of price vs. delivery time, histogram of delivery time, matrix of city × delivery speed.

---

## Getting Started

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows-only). For Mac users, run Power BI Desktop inside a Windows VM or use [Power BI Service](https://app.powerbi.com/) in the browser.

### Steps
1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/Swiggy-Restaurant-Data-Analysis.git
   cd Swiggy-Restaurant-Data-Analysis
   ```
2. Open `Swiggy Data Analysis.pbix` in Power BI Desktop.
3. If prompted, allow the report to use the bundled `swiggy.csv` as the data source (the path is relative and should resolve automatically).
4. Interact with the slicers, cross-filter the visuals, and export screenshots as needed.

> **Tip:** To refresh the data with a newer version of the CSV, replace `swiggy.csv` in the repo root, then in Power BI Desktop click **Home → Refresh**.

---

## Technologies Used

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Report authoring, DAX measures, dashboard visualization |
| **Power Query (M)** | ETL — cleaning, splitting, and shaping the raw CSV |
| **DAX** | Calculated columns and KPI measures |
| **CSV** | Source data format |
| **Git / GitHub** | Version control and project hosting |

---

## Data Source & Attribution

This project uses the publicly available **Swiggy Restaurant Dataset** published on Kaggle by Abhijit Dahatonde.

- **Dataset URL:** [https://www.kaggle.com/datasets/abhijitdahatonde/swiggy-restuarant-dataset](https://www.kaggle.com/datasets/abhijitdahatonde/swiggy-restuarant-dataset)
- **Author:** Abhijit Dahatonde
- **Platform:** Kaggle Datasets

> Please review the dataset's license on Kaggle before reusing the raw CSV for commercial purposes. The dataset is included in this repository for reproducibility of the Power BI report.

If you use this dataset in your own work, please credit the original Kaggle author.

---

## Future Enhancements

- [ ] Add time-series analysis once historical Swiggy data becomes available (current dataset is a snapshot).
- [ ] Build a Python ingestion layer (`pandas` + `matplotlib`) as an alternative to Power BI.
- [ ] Geocode `Address` and add a map visual for restaurant density.
- [ ] Build a Streamlit dashboard for users without Power BI Desktop.
- [ ] Add a cost-vs-rating quadrant chart to identify "value-for-money" clusters per city.

Contributions are welcome — feel free to open an issue or submit a pull request.

---
