
# World Population Demographics EDA

Exploratory analysis of the world population dataset using Python, Pandas, Matplotlib, and Seaborn.

This project started with basic EDA, but I extended it beyond surface-level inspection by creating population growth metrics, recalculating density, checking data consistency, and comparing countries across time.

The goal was not just to display charts, but to understand how population size, growth, density, and continent-level patterns connect with each other.

## What I Looked At

The dataset contains population records for countries and territories across multiple years:

* 1970
* 1980
* 1990
* 2000
* 2010
* 2015
* 2020
* 2022

I explored questions such as:

* Which countries have the largest populations in 2022?
* Which countries contribute the highest share of world population?
* How has population changed from 1970 to 2022?
* Which countries grew the most in absolute terms?
* Which countries grew the fastest in percentage terms?
* Which countries experienced population decline?
* How do continents compare in average population over time?
* Which numeric variables are strongly related?
* Which countries stand out as density or population outliers?

## Metrics Added

To move beyond basic sorting and charts, I added a few derived columns:

### Absolute Population Change

Measures the raw population increase or decrease between 1970 and 2022.

```python
df["abs_change_1970_2022"] = (
    df["2022 Population"] - df["1970 Population"]
)
```

This helps identify countries that added the largest number of people in absolute terms.

### Percentage Population Change

Measures growth relative to the 1970 population.

```python
df["pct_change_1970_2022"] = (
    (df["2022 Population"] - df["1970 Population"])
    / df["1970 Population"]
) * 100
```

This is useful because absolute growth can favor already large countries, while percentage growth shows relative expansion.

### Annualized Growth Rate

Calculates the average yearly growth rate from 1970 to 2022.

```python
df["annualized_cagr_pct"] = (
    (df["2022 Population"] / df["1970 Population"]) ** (1/52)
    - 1
) * 100
```

This gives a cleaner long-term growth comparison across countries.

### Recalculated Population Density

Checks population density using 2022 population and land area.

```python
df["density_calc_2022"] = (
    df["2022 Population"] / df["Area (km²)"]
)
```

This was added to validate the dataset’s density column and identify high-density countries and territories.

### Density Error Check

Compares calculated density with the density provided in the dataset.

```python
df["density_error_pct"] = (
    (df["density_calc_2022"] - df["Density (per km²)"])
    / df["Density (per km²)"]
) * 100
```

This helps flag possible rounding differences or data quality issues.

## Analysis Performed

The notebook includes:

* Dataset inspection using `info()` and `describe()`
* Missing value checks
* Unique value checks
* Sorting countries by population and world population share
* Correlation analysis across numeric columns
* Correlation heatmap
* Continent-level population aggregation
* Population trend comparison by continent
* Boxplot analysis for numeric distributions
* Population growth calculations
* Density validation
* Outlier detection using IQR
* Identification of countries with population decline

## Observations

China and India dominate the population rankings and heavily influence global population totals.

Population distribution is highly skewed. A few countries contain very large populations, while many countries and territories have much smaller populations.

Continent-level grouping shows that Asia has the largest population scale, while Oceania remains much smaller in comparison.

Population density tells a different story from total population. Some small territories and city-states have extremely high density even though their total population is not large.

Not every country grew between 1970 and 2022. Some countries and territories showed population decline, which makes the dataset more interesting than a simple “population always increases” story.

The correlation heatmap shows that population values across different years are strongly related, which makes sense because population changes gradually over time.

## Tools Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn

## Files

* `EDA_Pandas.ipynb` — main analysis notebook
* `world_population.csv` — source dataset

## Takeaway

This project helped me practice moving from basic EDA toward more meaningful analysis.

Instead of only checking summary statistics and plotting charts, I added derived metrics to compare countries by scale, growth rate, density, and long-term population change.

The main lesson from this project is that a dataset can look simple at first, but better questions make it more useful.
