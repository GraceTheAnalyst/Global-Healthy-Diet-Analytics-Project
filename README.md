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

## Data Sources


## Tools

- **Microsoft Excel** — initial data inspection
- **Python (pandas)** — data cleaning and correction
- **SQL** — querying and aggregation
- **Jupyter Notebook** — analysis environment
- **Plotly** — interactive data visualization

## Data Preparation/Cleaning

The raw dataset contained significant data quality issues. Upon inspection, the `region` column was found to be mislabeled for the vast majority of the 175 countries (for example, Argentina, Australia, Canada, and China were all incorrectly listed under "Africa"). The `cost_category` column also contained a large number of blank values.

To resolve this:
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

SQL was used to query and aggregate the cleaned dataset, generating regional averages, country rankings, and year-over-year trends. The aggregated results were then loaded into a Jupyter notebook, where Plotly was used to build five interactive visualizations:

1. Top 10 most expensive countries for a healthy diet
2. Average cost by region
3. Global cost trend over time (2017–2024)
4. Top 10 least expensive countries for a healthy diet
5. High Cost vs Medium Cost country counts by region

## Results/Findings

- **Most expensive:** Japan has the highest average daily cost for a healthy diet among all countries studied
- **Regional gap:** The Americas region has the highest average cost, while Europe is the most affordable on average
- **Rising costs:** The global average cost of a healthy diet has trended upward since 2017, with a sharper rise after 2020
- **Cost categories:** High Cost and Medium Cost countries are fairly evenly split overall, but distribution varies notably by region

## Recommendations

- Policymakers in high-cost regions, particularly in the Americas, should consider subsidies or interventions targeting fruit and vegetable affordability
- Future monitoring should track the post-2020 cost increase to determine whether it stabilizes or continues rising
- Organizations working on food security should prioritize the countries identified in the "most expensive" rankings for further investigation

## Limitations

- Several rows had missing values for vegetable, fruit, and total food component costs, so those specific breakdowns should be interpreted with caution
- The dataset measures cost only, not affordability relative to income, so it does not capture how burdensome these costs are for local populations
- Some country-level values are marked as "estimated" rather than directly measured, which may affect precision

---

## Author

Built as a learning project to practice a complete data analysis pipeline from raw, messy data through cleaning, querying, and interactive visualization.
