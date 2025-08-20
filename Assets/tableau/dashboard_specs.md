# Tableau Dashboard Specifications

## Dashboard Components

### 1. Time Series Chart
- **Type**: Line chart with area fill
- **X-axis**: Date (continuous)
- **Y-axis**: New cases (linear scale)
- **Color**: Country/Location
- **Filters**: Date range, Country selection
- **Features**: Hover tooltips, zoom functionality

### 2. Global Map
- **Type**: Filled map
- **Geography**: Countries
- **Color**: Total cases (graduated color scale)
- **Size**: Total deaths
- **Filters**: Date slider
- **Features**: Popup details on hover

### 3. Country Comparison
- **Type**: Horizontal bar chart
- **X-axis**: Total cases
- **Y-axis**: Countries (sorted by cases)
- **Color**: Region/Continent
- **Features**: Top N filter

### 4. KPI Cards
- **Total Global Cases**: Sum aggregation
- **Total Global Deaths**: Sum aggregation  
- **Case Fatality Rate**: Calculated field (deaths/cases)
- **Countries Affected**: Count distinct locations

## Design Specifications
- **Color Palette**: Blue-Red gradient for cases, Orange-Red for deaths
- **Font**: Tableau Book (default)
- **Layout**: 1920x1080 dashboard size
- **Interactivity**: Cross-filtering between charts
- **Responsive**: Desktop and tablet optimized