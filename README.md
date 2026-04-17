# After COVID: Healthcare Access & Income Inequality in California

**DATA 271 · Data Wrangling & Visualization · Cal Poly Humboldt · Spring 2026**

---

## Overview

This project examines whether the COVID-19 pandemic permanently widened healthcare access gaps between low- and high-income Californians. Using U.S. Census ACS data across all 58 California counties from 2018 to 2023, we compare pre-pandemic (2018–2019) and post-pandemic (2021–2023) trends in uninsured rates, poverty rates, housing cost burden, and median income — segmented by county poverty level.

The analysis is framed around a core question: **did income growth after COVID actually translate to improved economic security and healthcare access, or did rising costs absorb those gains?**

---

## Key Findings

- **Median income rose steadily** across all counties from 2018 to 2023, but this did not produce consistent improvements in other economic indicators
- **Housing cost burden increased post-2020**, particularly in high-poverty counties, suggesting that income gains were offset by rising costs
- **Poverty and uninsured rates plateaued after 2020** rather than continuing their pre-pandemic declining trend
- **High-poverty counties consistently bore greater cost burdens** than low-poverty counties in every year studied — the gap did not narrow post-pandemic
- A newly engineered **income-after-housing** metric revealed that effective purchasing power remains constrained despite nominal income growth

---

## Dataset

**Source:** U.S. Census Bureau — American Community Survey (ACS)
[data.census.gov](https://data.census.gov)

| Variable | Description |
|----------|-------------|
| `County` | All 58 California counties |
| `Year` | 2018–2023 (6 years) |
| `Population` | County population estimate |
| `Median Income` | Median household income (USD) |
| `Poverty Rate` | Percentage of residents below poverty line |
| `Unemployment Rate` | County unemployment rate |
| `Uninsured Rate` | Percentage of residents without health insurance |
| `Cost Burden Rate` | Share of households spending >30% of income on housing |

**Size:** 348 rows × 8 columns (58 counties × 6 years)

The dataset was assembled by pulling annual ACS county-level tables for each year and combining them into a single panel dataset.

---

## Methods

### Data Cleaning
- Stripped formatting characters (`%`, `$`, `,`) from numeric columns stored as strings
- Converted all rate columns to float decimals (e.g., `10.6%` → `0.106`)
- Standardized column names to snake_case
- Checked for and confirmed no duplicate or missing rows

### Feature Engineering
Two new columns were created to support the analysis:

| Column | Type | Definition |
|--------|------|------------|
| `poverty_level` | Categorical | `"High Poverty"` if `poverty_rate ≥ 15%`, else `"Low Poverty"` |
| `income_after_housing` | Numerical | `median_income × (1 − cost_burden_rate)` — estimated take-home income after housing costs |

### Exploratory Data Analysis
- **Trend plots** — median income, poverty rate, and uninsured rate over time (2018–2023)
- **Grouped line plot** — cost burden rate over time, split by poverty level (faceted by `hue=`)
- **Dual-axis trend** — poverty rate vs. uninsured rate overlaid to compare trajectories
- **Grouped aggregation** — yearly averages by poverty classification to quantify the gap

---

## Visualizations

Key charts produced in the notebook:

1. **Median Income Over Time** — statewide average across all 58 counties
2. **Cost Burden Rate by Poverty Level** — grouped line plot showing high vs. low poverty counties diverging post-2020
3. **Poverty vs. Uninsured Rate Over Time** — dual trend showing plateau effect after pandemic

---

## Files

| File | Description |
|------|-------------|
| `midterm2_takehome.ipynb` | Full analysis notebook — cleaning, EDA, feature engineering, visualizations |
| `california_county_data.csv` | Cleaned dataset: 58 CA counties × 6 years (2018–2023), 8 variables from U.S. Census ACS |

---

## Tech Stack

`Python` · `Pandas` · `NumPy` · `Matplotlib` · `Seaborn` · `Jupyter Notebook`

---

## How to Run

1. Clone the repo or download the files
2. Place `california_county_data.csv` in the same directory as the notebook
3. Open `midterm2_takehome.ipynb` in Jupyter or Google Colab
4. Run all cells top to bottom

> No API keys or external dependencies required — the dataset is included in the repo.

---

## Limitations & Future Work

- The dataset combines ACS variables that were pulled separately per year — minor methodology changes in ACS collection between years may introduce noise
- Cost burden rate is a housing-specific measure and does not capture all cost-of-living dimensions
- Future work could incorporate CDC BRFSS data on self-reported healthcare access and foregone care due to cost, enabling a more direct measure of healthcare barriers beyond insurance status
- Urban vs. rural segmentation could reveal geographic patterns not visible at the county level

---

## Authors

Katayoon Seraji Nezhad · Justin Arellano
Cal Poly Humboldt — DATA 271, Spring 2026
