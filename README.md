# Chicago Food Inspections: Data Visualization and Analysis

An end-to-end data analysis project exploring food safety trends across Chicago zip codes from 2010 to 2026, using inspection records from the City of Chicago Data Portal.

## Research Question

> Do high-risk geographic clusters show meaningful improvement over time, or do they remain consistent sources of elevated violations?

## Dataset

- **Source:** [City of Chicago Data Portal — Food Inspections](https://data.cityofchicago.org/Health-Human-Services/Food-Inspections/4ijn-s7e5/about_data)
- **Size:** ~310,000 inspection records across 17 columns
- **Coverage:** 2010–2026, managed by the Chicago Department of Public Health's Food Protection Program

## Project Structure

```
chicago-food-inspections/
├── data/
│   ├── raw/                  # Original dataset from Chicago Data Portal
│   └── processed/            # Cleaned and aggregated data
├── notebooks/
│   ├── 01_cleaning.ipynb     # Data cleaning and preparation
│   ├── 02_eda.ipynb          # Exploratory visualizations
│   └── 03_analysis.ipynb     # Final analysis and time-series plots
├── visuals/                  # Exported figures and interactive HTML plots
└── README.md
```

## Methods

### Data Cleaning
- Handled 90,000+ missing values with column-specific strategies
- Removed out-of-state records (Wisconsin, Indiana, California) to keep scope within Chicago
- Standardized the `Facility Type` column into five categories: Restaurant, Grocery Store, Convenience Store, Children's Services Facility, and Pharmacy
- Removed failed inspections with missing violation reports (~1% of data) and records with missing coordinates (~0.3%)

### Feature Engineering
The dataset was aggregated by zip code and risk level, generating metrics including:
- `failure_rate` — proportion of inspections resulting in failure
- `violations_per_inspection` — average violations across all inspections
- `violations_per_fail` — average violations recorded only at failures
- `risk_proportion` — share of each risk tier within each zip code

### Analysis
- Exploratory boxplots and correlation matrices to validate risk classification against violation metrics
- Geospatial choropleth map of Chicago zip codes colored by average violations per failure
- Interactive monthly time-series plots (2010–2026) with year slider
- Yearly mean and median trend lines for three high-risk target zip codes: **60614, 60616, 60659**

## Key Findings

- Failure rate (~18%) is roughly uniform across all three risk levels — it is **not** a reliable indicator of risk classification
- Violations per failure increases meaningfully with risk level, confirming it as a stronger signal
- All three target zip codes show a sharp increase in violations per failure beginning in **2018**, coinciding with a change in inspection procedures by the City of Chicago
- During **2020**, violations per failure spiked sharply within target Zip code areas, likely influenced by COVID-19 pandemic disruptions
- As of 2024, all three high-risk zip codes continue to record months above 8 violations per failure, well above the city average of 6

## Limitations

- A procedural change to food inspections in July 2018 significantly impacts pre/post comparability; details are unavailable due to an expired link on the Data Portal
- High qualitative variability in `Facility Type` (363 unique values) and `Inspection Type` (86 unique values) limits linear tracking of individual business outcomes
- Some zero-violation months in 60616 are likely artifacts of missing data rather than genuine improvement

## Requirements

```
pandas
geopandas
matplotlib
seaborn
plotly
numpy
```

## Usage

```bash
git clone https://github.com/ellis-jace/chicago-food-inspections.git
cd chicago-food-inspections
pip install -r requirements.txt
jupyter notebook notebooks/cleaning.ipynb
```

## References

- City of Chicago (2026). *Food Inspections Data.* https://data.cityofchicago.org/Health-Human-Services/Food-Inspections/4ijn-s7e5/about_data
- U.S. Census Bureau (2020). *Total Population Estimate.* https://worldpopulationreview.com/us-cities 
