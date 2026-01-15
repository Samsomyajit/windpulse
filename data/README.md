# Data Directory

This directory is for storing wind farm data files used in the analysis.

## 📋 Data Format

### Required Format

Wind data should be provided in **Excel (.xlsx)** format with the following structure:

| YEAR | MN | DT | S01  | S02  | S03  | ... | S24  |
|------|----|----|------|------|------|-----|------|
| 2020 | 1  | 1  | 12.5 | 11.8 | 10.9 | ... | 14.2 |
| 2020 | 1  | 2  | 13.1 | 12.3 | 11.5 | ... | 15.0 |
| 2020 | 1  | 3  | 11.9 | 11.2 | 10.5 | ... | 13.8 |
| ...  | ...| ...| ...  | ...  | ...  | ... | ...  |

### Column Descriptions

- **YEAR**: Year of measurement (e.g., 2020)
- **MN**: Month number (1-12)
- **DT**: Day of month (1-31)
- **S01-S24**: Hourly wind speed measurements in **km/h**
  - S01 = Hour 0 (midnight to 1 AM)
  - S02 = Hour 1 (1 AM to 2 AM)
  - ...
  - S24 = Hour 23 (11 PM to midnight)

### Data Requirements

- **Units**: Wind speed in km/h (will be converted to m/s in analysis)
- **Hub Height**: Data should be at 10 meters hub height
- **Temporal Coverage**: At least 1 year of continuous data recommended
- **Data Quality**: 
  - No missing values (or use appropriate fill method)
  - Realistic wind speed ranges (0-100 km/h typically)
  - Consistent measurement intervals

## 📁 File Organization

Recommended file naming convention:

```
data/
├── location1_2020_winddata.xlsx
├── location1_2021_winddata.xlsx
├── location2_2020_winddata.xlsx
├── location2_2021_winddata.xlsx
└── sample_data_format.xlsx (example template)
```

## 🔢 Sample Data

### Creating Sample Data

A Python script to generate sample data for testing:

```python
import pandas as pd
import numpy as np

# Generate sample wind data
np.random.seed(42)
dates = pd.date_range('2020-01-01', '2020-12-31', freq='D')

data = {
    'YEAR': dates.year,
    'MN': dates.month,
    'DT': dates.day,
}

# Generate hourly wind speeds (km/h) with diurnal pattern
for hour in range(1, 25):
    # Simulate diurnal pattern: lower at night, higher during day
    base = 12  # Base wind speed
    diurnal_factor = 5 * np.sin(2 * np.pi * (hour - 6) / 24)
    seasonal_factor = 3 * np.sin(2 * np.pi * dates.month / 12)
    random_noise = np.random.normal(0, 2, len(dates))
    
    wind_speed = np.maximum(0, base + diurnal_factor + seasonal_factor + random_noise)
    data[f'S{hour:02d}'] = wind_speed

df = pd.DataFrame(data)
df.to_excel('sample_wind_data.xlsx', index=False)
print("Sample data created: sample_wind_data.xlsx")
```

## 📊 Data Sources

### Indian Meteorological Department (IMD)
- Official source for Indian weather data
- Website: https://www.imd.gov.in/
- Contact IMD for access to wind data

### Other Sources
- National Institute of Wind Energy (NIWE)
- State nodal agencies
- Wind farm SCADA systems
- Research institutions

## 🔒 Data Privacy

**Important**: Do not commit sensitive or proprietary data to the repository!

The `.gitignore` file is configured to exclude:
- `*.xlsx` - Excel files
- `*.xls` - Old Excel format
- `*.csv` - CSV files
- `data/` - This entire directory

### Sharing Data Safely

For sharing example data:
1. Create synthetic/anonymized data
2. Get explicit permission from data owners
3. Use only publicly available datasets
4. Document data sources and licenses

## 🔄 Data Preprocessing

Before analysis, data should be:

1. **Validated**: Check for missing values and outliers
2. **Cleaned**: Remove or interpolate invalid measurements
3. **Standardized**: Ensure consistent units and formats
4. **Documented**: Include metadata about collection methods

### Example Preprocessing Script

```python
import pandas as pd
import numpy as np

def validate_wind_data(filepath):
    """Validate wind data file format and content."""
    df = pd.read_excel(filepath)
    
    # Check required columns
    required_cols = ['YEAR', 'MN', 'DT'] + [f'S{i:02d}' for i in range(1, 25)]
    missing_cols = set(required_cols) - set(df.columns)
    if missing_cols:
        raise ValueError(f"Missing columns: {missing_cols}")
    
    # Check wind speed ranges
    wind_cols = [f'S{i:02d}' for i in range(1, 25)]
    wind_data = df[wind_cols]
    
    if (wind_data < 0).any().any():
        print("Warning: Negative wind speeds found")
    if (wind_data > 100).any().any():
        print("Warning: Unusually high wind speeds found (> 100 km/h)")
    
    # Check for missing values
    if df.isnull().any().any():
        print(f"Warning: Missing values found: {df.isnull().sum().sum()} cells")
    
    print(f"✓ Data validation complete for {filepath}")
    return True

# Usage
validate_wind_data('location1_2020_winddata.xlsx')
```

## 📈 Data Statistics

### Typical Wind Characteristics in India

| Region | Mean Wind Speed | Peak Season | Hub Height |
|--------|----------------|-------------|------------|
| Tamil Nadu | 6-8 m/s | May-Sep | 80-120 m |
| Gujarat | 5-7 m/s | Jun-Sep | 80-100 m |
| Karnataka | 5-7 m/s | Jun-Sep | 80-100 m |
| Rajasthan | 4-6 m/s | May-Aug | 80-120 m |
| Maharashtra | 5-7 m/s | Jun-Sep | 80-100 m |

*Note: Our analysis uses 10m hub height for consistency with IMD data*

## 🛠️ Data Processing Tools

### Recommended Tools

- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computations
- **OpenPyXL**: Excel file handling
- **SciPy**: Statistical analysis

### Installation

```bash
pip install pandas numpy openpyxl scipy
```

## 📝 Data Citation

If you use IMD or other public data sources, please cite appropriately:

```
Indian Meteorological Department (IMD)
Ministry of Earth Sciences, Government of India
https://www.imd.gov.in/
```

## 🤝 Contributing Data

To contribute anonymized data for research:

1. Ensure you have permission to share
2. Anonymize location-specific information
3. Document data collection methods
4. Contact repository maintainers
5. Follow data sharing agreements

## 📞 Support

For data-related questions:
- Check this README first
- Review the [main documentation](../docs/)
- Open an issue on [GitHub](https://github.com/Samsomyajit/windpulse/issues)

---

**Note**: This directory is excluded from version control by `.gitignore` to prevent accidental commits of large data files.
