# Data Dictionary

## Overview
This document provides comprehensive definitions for all variables used in the COVID-19 Global Analysis Dashboard project.

## Primary Dataset: Our World in Data COVID-19 Database

### Source Information
- **Provider**: Our World in Data (OWID)
- **URL**: https://ourworldindata.org/covid-deaths
- **License**: Creative Commons BY license
- **Update Frequency**: Daily


## Variable Definitions

### Core Variables

| Variable Name | Data Type | Description | Example | Units | Notes |
|---------------|-----------|-------------|---------|-------|--------|
| `iso_code` | String | ISO 3166-1 alpha-3 country code | "USA", "GBR" | - | Standard country identifier |
| `continent` | String | Continent name | "Asia", "Europe" | - | Geographic grouping |
| `location` | String | Country or region name | "United States", "World" | - | Primary geographic identifier |
| `date` | Date | Reporting date | 2023-03-15 | YYYY-MM-DD | Daily frequency |
| `population` | Integer | Total population | 331,900,000 | People | Latest available estimate |

### Case Variables

| Variable Name | Data Type | Description | Example | Units | Notes |
|---------------|-----------|-------------|---------|-------|--------|
| `total_cases` | Integer | Cumulative confirmed cases | 1,000,000 | Cases | Running total since start |
| `new_cases` | Integer | New confirmed cases | 1,234 | Cases/day | Daily increment |
| `new_cases_smoothed` | Float | 7-day rolling average of new cases | 1,156.7 | Cases/day | Smoothed for trend analysis |
| `total_cases_per_million` | Float | Cumulative cases per million population | 3,015.2 | Cases/1M pop | Population-adjusted |
| `new_cases_per_million` | Float | New cases per million population | 3.72 | Cases/1M pop/day | Population-adjusted daily |

### Death Variables

| Variable Name | Data Type | Description | Example | Units | Notes |
|---------------|-----------|-------------|---------|-------|--------|
| `total_deaths` | Integer | Cumulative confirmed deaths | 10,000 | Deaths | Running total since start |
| `new_deaths` | Integer | New confirmed deaths | 25 | Deaths/day | Daily increment |
| `new_deaths_smoothed` | Float | 7-day rolling average of new deaths | 23.4 | Deaths/day | Smoothed for trend analysis |
| `total_deaths_per_million` | Float | Cumulative deaths per million population | 30.15 | Deaths/1M pop | Population-adjusted |
| `new_deaths_per_million` | Float | New deaths per million population | 0.075 | Deaths/1M pop/day | Population-adjusted daily |

### Testing Variables

| Variable Name | Data Type | Description | Example | Units | Notes |
|---------------|-----------|-------------|---------|-------|--------|
| `total_tests` | Integer | Cumulative tests performed | 500,000,000 | Tests | May include multiple test types |
| `new_tests` | Integer | New tests performed | 1,500,000 | Tests/day | Daily testing volume |
| `positive_rate` | Float | Percentage of tests that are positive | 0.05 | Proportion | Range: 0-1 |
| `tests_per_case` | Float | Tests performed per confirmed case | 20.0 | Tests/case | Inverse of positive rate |

### Derived Variables (Created in Analysis)

| Variable Name | Data Type | Description | Calculation | Units | Purpose |
|---------------|-----------|-------------|-------------|-------|---------|
| `year` | Integer | Year extracted from date | `date.year` | Year | Temporal grouping |
| `month` | Integer | Month extracted from date | `date.month` | Month (1-12) | Seasonal analysis |
| `quarter` | Integer | Quarter extracted from date | `date.quarter` | Quarter (1-4) | Quarterly trends |
| `day_of_year` | Integer | Day of year | `date.dayofyear` | Day (1-366) | Seasonal patterns |
| `day_of_week` | String | Day name | `date.day_name()` | Day name | Weekly patterns |
| `case_fatality_rate` | Float | Deaths divided by cases | `total_deaths/total_cases` | Proportion | Severity indicator |
| `growth_rate` | Float | Daily percentage change in cases | `new_cases.pct_change()` | Percentage | Transmission dynamics |
| `doubling_time` | Float | Days for cases to double | `log(2)/log(1+growth_rate)` | Days | Epidemic speed |

## Data Quality Indicators

### Completeness Metrics
| Variable | Completeness % | Missing Count | Strategy |
|----------|----------------|---------------|----------|
| `location` | 100% | 0 | Complete |
| `date` | 100% | 0 | Complete |
| `new_cases` | 95.2% | 2,341 | Forward/backward fill |
| `new_deaths` | 93.8% | 3,012 | Forward/backward fill |
| `total_cases` | 98.7% | 634 | Cumulative calculation |

### Data Processing Notes

#### Missing Value Treatment
1. **Essential Variables**: Rows dropped if missing (location, date)
2. **Numerical Variables**: Forward fill then backward fill by location
3. **Derived Variables**: Calculated after missing value treatment

#### Outlier Handling
1. **Statistical Outliers**: Identified but retained with flagging
2. **Contextual Analysis**: Verified against known events
3. **Robust Statistics**: Used median/IQR for central tendency

#### Data Validation Rules
- `new_cases >= 0` (non-negative constraint)
- `total_cases >= previous_day_total_cases` (monotonic constraint)
- `date` within expected range (2020-01-01 to present)
- `location` matches ISO country codes

## Usage Guidelines

### Recommended Applications
- ✅ Time series analysis and forecasting
- ✅ Cross-country comparative studies
- ✅ Seasonal pattern identification
- ✅ Dashboard and visualization development

### Limitations & Cautions
- ⚠️ Testing capacity varies significantly between countries
- ⚠️ Reporting standards may differ across regions
- ⚠️ Case numbers represent detected cases, not total infections
- ⚠️ Death counts may have varying lag times and definitions

### Citation Requirements
When using this data, please cite:
```
Mathieu, E., Ritchie, H., Ortiz-Ospina, E. et al. A global database of COVID-19 vaccinations. Nat Hum Behav (2021). https://doi.org/10.1038/s41562-021-01122-8
```