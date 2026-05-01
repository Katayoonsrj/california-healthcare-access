# Healthcare Access Inequality in California Before and After COVID-19

**Course:** DATA 271 — Data Wrangling | Cal Poly Humboldt | Spring 2026  
**Authors:** Katayoon Seraji Nezhad · Justin Arellano

---

## Overview

This project examines whether the COVID-19 pandemic widened pre-existing healthcare access inequalities across California's 58 counties. Using U.S. Census Bureau data from 2018 to 2023, we compare uninsured rates, poverty, housing cost burden, and median income before (2018–2019) and after (2021–2023) the pandemic, with a focus on whether high-poverty counties experienced different trajectories than low-poverty counties.

All data is fetched programmatically from the Census Bureau API — no manual spreadsheet work is involved.

---

## Research Question

> Did the COVID-19 pandemic widen healthcare access disparities across California counties, and did economic recovery benefit high-poverty and low-poverty counties equally?

---

## Data Source

**U.S. Census Bureau — American Community Survey (ACS) 5-Year Estimates**  
[data.census.gov](https://data.census.gov/table?q=california&g=010XX00US$0500000)

The ACS 5-year product is used because it covers all 58 California counties, including small rural counties with populations below the 65,000-person threshold required for ACS 1-year publication.

| Variable | ACS Code | Definition |
|----------|----------|------------|
| Population | `B01003_001E` | Total population estimate |
| Median Income | `B19013_001E` | Median household income ($) |
| Poverty Rate | `S1701_C03_001E` | % of people below the federal poverty level |
| Unemployment Rate | `S2301_C04_001E` | % of civilian labor force (16+) unemployed |
| Uninsured Rate | `S2701_C05_001E` | % of people with no health insurance |
| Cost Burden Rate | `DP04_0142PE` | % of housing units spending ≥30% of income on housing |

**CPI data** (for inflation adjustment) is fetched from the [Bureau of Labor Statistics API](https://www.bls.gov/developers/) — series `CUUR0000SA0`.

---

## Notebook Structure

| Section | Description |
|---------|-------------|
| 1. Introduction | Research question and motivation |
| 2. Required Libraries | All imports with descriptions |
| 3. Data Preparation | Census API extraction across 6 years and 3 table types |
| 4. Data Cleaning | Sentinel handling, dtype fixes, missing values, period labeling |
| 5. Summary Statistics | Descriptive stats and year-by-year trend table |
| 6. Column Engineering | `poverty_level` (categorical) and `income_after_housing` (numeric) |
| 7. Visualizations | 5 plots with interpretations |
| 8. Grouped Analysis | Pre- vs. post-pandemic comparison by poverty level |
| 9. Summary of Findings | Key findings and open questions |
| Bonus | CPI inflation adjustment via BLS API |

---

## Key Findings

- The statewide uninsured rate declined from ~7–8% in 2018 to ~5–6% by 2023, and median income rose throughout — but this aggregate improvement masks significant county-level inequality.
- High-poverty counties (poverty rate ≥15%) maintained uninsured rates approximately **twice** those of low-poverty counties across the entire 2018–2023 period, and this gap did not meaningfully narrow post-pandemic.
- Housing cost burden rose **every single year** for all counties, with both poverty groups exceeding the HUD 30% cost-burdened threshold throughout — no pandemic-era policy interrupted this trend.
- The county-level comparison (Trinity vs. Humboldt vs. Santa Clara) shows the full range: the highest-income county converged toward near-universal coverage while the lowest-income county remained near double the statewide average even in 2023.

---

## Visualizations

1. Median income vs. uninsured rate over time (dual-axis)
2. Uninsured rate by poverty level over time (grouped line plot)
3. Poverty rate vs. uninsured rate — decoupling post-pandemic
4. Housing cost burden by poverty level over time
5. Faceted county comparison: Trinity · Humboldt · Santa Clara

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
requests
```

Install with:
```bash
pip install pandas numpy matplotlib seaborn requests
```

---

## How to Run

1. Clone the repository
2. Open `DATA271_Final_Project.ipynb` in JupyterHub or Jupyter Notebook
3. Run all cells — data is fetched live from the Census and BLS APIs, no local data files needed

> **Note:** The Census API key is included in the notebook. For your own projects, register for a free key at [api.census.gov/data/key_signup.html](https://api.census.gov/data/key_signup.html).

---

## Repository Structure

```
├── DATA271_Final_Project.ipynb   # Main analysis notebook
└── README.md
```

---

*Cal Poly Humboldt · DATA 271 · Spring 2026*
