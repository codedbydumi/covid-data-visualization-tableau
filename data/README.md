# Data Directory

## Structure
- `raw/` - Original, unmodified datasets
- `processed/` - Cleaned and transformed data ready for analysis

## Data Sources
- **owid-covid-data.csv**: COVID-19 data from Our World in Data
  - Source: https://ourworldindata.org/covid-deaths
  - License: Creative Commons BY license
  - Last Updated: [Date]

## Data Dictionary
| Column | Description | Type | Example |
|--------|-------------|------|---------|
| location | Country/region name | string | "United States" |
| date | Reporting date | date | 2023-03-15 |
| new_cases | Daily new cases | integer | 1,234 |
| total_cases | Cumulative cases | integer | 1,000,000 |
| new_deaths | Daily new deaths | integer | 25 |
| total_deaths | Cumulative deaths | integer | 10,000 |

## Usage Notes
- Missing values handled using forward/backward fill
- Outliers identified using IQR and Z-score methods
- Data covers period: 2020-01-01 to 2023-12-31