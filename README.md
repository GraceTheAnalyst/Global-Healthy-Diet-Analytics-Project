# Global Healthy Diet Analytics Project

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Preparation/Cleaning](#data-preparationcleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

---

## Project Overview

This data analysis project explores the cost of maintaining a healthy diet across 175 countries from 2017 to 2024. By analyzing cost patterns across regions and over time, this project seeks to identify which parts of the world face the highest and lowest costs for healthy eating, how those costs have changed over the past several years, and what data quality challenges affect this kind of global analysis.

<img width="1296" height="505" alt="Screenshot (47" src="https://github.com/user-attachments/assets/3494029d-3ee7-44a1-97df-76d9af4042cf" />


## Data Sources
The dataset used for this analysis is:
[price_of_healthy_diet_clean.csv](price_of_healthy_diet_clean.csv)

## Tools

- **Microsoft Excel** — initial data inspection
- **Python (pandas)** — data cleaning and correction
- **SQL** — querying and aggregation
- **Jupyter Notebook** — analysis environment
- **Plotly** — interactive data visualization

## Data Preparation/Cleaning

The raw dataset contained significant data quality issues. Upon inspection, the `region` column was found to be mislabeled for the vast majority of the 175 countries.

- Each country's region was manually verified and corrected based on actual geography
- Missing `cost_category` values were filled in using the median daily diet cost as a threshold, classifying countries above the median as "High Cost" and below as "Medium Cost"
- Duplicate rows were checked and removed

## Exploratory Data Analysis

Initial exploration in SQL focused on understanding the shape and distribution of the data:
- Average daily diet cost by region
- Highest and lowest cost countries
- Year-over-year cost trends from 2017 to 2024
- Distribution of High Cost vs Medium Cost countries by region

## Data Analysis

A few snippets from the project that solved interesting problems along the way.

**Fixing 175 mislabeled regions with a single lookup**

The original dataset had countries assigned to the wrong region almost entirely. Rather than fixing rows one by one, a dictionary mapping every country to its correct region was built and applied in one line:

```python
df['region'] = df['country'].map(region_map)
```

**Filling missing cost categories based on the data**

Instead of manually labeling blank cost categories, the median cost was used as a natural dividing line:

```python
median_cost = df['cost_healthy_diet_ppp_usd'].median()

df['cost_category'] = df['cost_healthy_diet_ppp_usd'].apply(
    lambda x: 'High Cost' if x >= median_cost else 'Medium Cost'
)
```

**Aggregating cost trends by year in SQL**

```sql
SELECT year,
       ROUND(AVG(cost_healthy_diet_ppp_usd), 2) AS avg_daily_cost
FROM diet_costs
GROUP BY year
ORDER BY year ASC;
```

**Turning a SQL ranking query into an interactive chart**

```python
top10 = df_full.groupby('country')['cost_healthy_diet_ppp_usd'].mean().sort_values(ascending=False).head(10).reset_index()

fig = px.bar(top10, x='cost_healthy_diet_ppp_usd', y='country', orientation='h',
             title='Top 10 Most Expensive Countries for a Healthy Diet',
             color='cost_healthy_diet_ppp_usd', color_continuous_scale='Blues')
fig.update_layout(yaxis={'categoryorder': 'total ascending'})
fig.show()
```
## Results/Findings

- **Most expensive:** Japan has the highest average daily cost for a healthy diet among all countries studied

<img width="1270" height="480" alt="Screenshot (44" src="https://github.com/user-attachments/assets/9d23e140-861b-4ec1-8024-54be6dda2936" />

  
- **Regional gap:** The Americas region has the highest average cost, while Europe is the most affordable on average

<img width="1183" height="523" alt="Screenshot (45" src="https://github.com/user-attachments/assets/3907c3c5-78fe-460c-ae57-00814f90576d" />


- **Rising costs:** The global average cost of a healthy diet has trended upward since 2017, with a sharper rise after 2020

<img width="1231" height="489" alt="Screenshot (46" src="https://github.com/user-attachments/assets/7eec5265-2d71-47a4-9c74-d3eff6b62222" />


- **Cost categories:** High Cost and Medium Cost countries are fairly evenly split overall, but distribution varies notably by region

<img width="1074" height="481" alt="Screenshot 49" src="https://github.com/user-attachments/assets/cc14c449-9b81-4cd8-91a4-cc1f3848d242" />


## Recommendations

- Policymakers in high-cost regions should consider subsidies or interventions targeting fruit and vegetable affordability
- Future monitoring should track the post-2020 cost increase to determine whether it stabilizes or continues rising

## Limitations

- Several rows had missing values for vegetable, fruit, and total food component costs, so those specific breakdowns should be interpreted with caution
- The dataset measures cost only, not affordability relative to income, so it does not capture how burdensome these costs are for local populations
- Some country-level values are marked as "estimated" rather than directly measured, which may affect precision

---

## Author

Built as a learning project to practice a complete data analysis pipeline from raw, messy data through cleaning, querying, and interactive visualization.
