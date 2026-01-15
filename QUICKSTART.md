# Quick Start Guide

This guide will help you get started with WindPulse wind power density analysis.

## Prerequisites

- Python 3.8 or higher
- pip package manager
- Jupyter Notebook (for running analysis notebooks)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Samsomyajit/windpulse.git
cd windpulse
```

### 2. Create Virtual Environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Linux/Mac:
source venv/bin/activate

# On Windows:
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## Running the Analysis

### Option 1: Jupyter Notebook (Recommended)

1. Start Jupyter Notebook:
```bash
jupyter notebook
```

2. Open `meintanance_wpd.ipynb` in the browser

3. Run cells sequentially or run all cells:
   - Menu: Cell → Run All

### Option 2: Command Line Execution

```bash
# Execute the notebook and save output
jupyter nbconvert --to notebook --execute meintanance_wpd.ipynb --output meintanance_wpd_executed.ipynb
```

## Data Format

### Input Data Requirements

Your wind data should be in Excel format with the following structure:

| YEAR | MN | DT | S01 | S02 | ... | S24 |
|------|----|----|-----|-----|-----|-----|
| 2020 | 1  | 1  | 12.5| 11.3| ... | 15.2|
| 2020 | 1  | 2  | 13.1| 12.8| ... | 14.9|

Where:
- **YEAR**: Year of measurement
- **MN**: Month (1-12)
- **DT**: Day of month (1-31)
- **S01-S24**: Hourly wind speed measurements in km/h (hours 0-23)

### Preparing Your Data

1. Place your Excel files in a data directory
2. Ensure column names match the expected format
3. Wind speeds should be in km/h at 10m hub height

## Understanding the Output

### Generated Visualizations

After running the analysis, you'll get 60+ visualizations in the output:

1. **Contour Heat Maps** (Images 1-5)
   - Show wind power density variations across time and months
   - Identify optimal maintenance windows visually

2. **Individual Site Analysis** (Images 6-41)
   - Maintenance recommendation strips
   - Seasonal diurnal profiles
   - Risk-loss trade-off curves
   - Statistical distributions

3. **Multi-Site Comparisons** (Images 42-46)
   - Compare multiple locations side-by-side
   - Identify regional patterns

4. **Clustering Analysis** (Images 49-58)
   - Site groupings based on wind patterns
   - PCA, t-SNE, and UMAP visualizations

### Extracting Images

To extract images from the notebook:

```python
import json
import base64
import os

# Read the notebook
with open('meintanance_wpd.ipynb', 'r') as f:
    notebook = json.load(f)

# Create output directory
os.makedirs('extracted_images', exist_ok=True)

# Extract images
image_count = 0
for cell in notebook.get('cells', []):
    if cell.get('cell_type') == 'code':
        for output in cell.get('outputs', []):
            data = output.get('data', {})
            if 'image/png' in data:
                image_count += 1
                filename = f'extracted_images/image_{image_count:03d}.png'
                with open(filename, 'wb') as img_file:
                    img_file.write(base64.b64decode(data['image/png']))
                print(f"Extracted: {filename}")
```

## Interpreting Results

### Optimal Maintenance Windows

The analysis identifies optimal maintenance windows based on:

1. **Mean WPD**: Average wind power density
2. **Risk Level**: Probability of favorable conditions
3. **Consistency**: How reliable the window is across years

**Green zones** in maintenance strip plots indicate optimal times for maintenance.

### Clustering Results

Sites are grouped into clusters (A, B, C, etc.) based on similarity. Sites in the same cluster:
- Have similar diurnal wind patterns
- Can coordinate maintenance schedules
- May share resources efficiently

### Power Loss Estimates

The analysis provides:
- Expected power loss for each maintenance window
- Comparison vs. random scheduling
- Risk-adjusted recommendations

## Customizing the Analysis

### Adjusting Parameters

Key parameters you can modify in the notebook:

```python
# Hub height (meters)
HUB_HEIGHT = 10

# Risk parameters
WINDOW_H = 6          # Maintenance window length (hours)
PROB_TARGET = 0.70    # Target probability threshold
BOOT_B = 1000         # Bootstrap iterations

# Visualization
COLORMAP = 'viridis'  # Color scheme for plots
DPI = 300             # Resolution for saved figures
```

### Adding New Locations

1. Prepare data in the required format
2. Add location name to the site list
3. Update file paths in the notebook
4. Re-run the analysis

## Troubleshooting

### Common Issues

**Issue**: Module not found error
```
Solution: Ensure all dependencies are installed
pip install -r requirements.txt
```

**Issue**: Memory error with large datasets
```
Solution: Reduce the number of bootstrap iterations
BOOT_B = 100  # Instead of 1000
```

**Issue**: Images not displaying in notebook
```
Solution: Ensure matplotlib backend is set correctly
%matplotlib inline
```

**Issue**: Excel file read error
```
Solution: Install openpyxl
pip install openpyxl
```

## Next Steps

1. **Explore Documentation**: Visit the [project website](https://samsomyajit.github.io/windpulse/)
2. **View Examples**: Check the [gallery](docs/gallery.md) for visualization examples
3. **Read Methodology**: Understand the [detailed methodology](docs/methodology.md)
4. **Contribute**: See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines

## Getting Help

- **Issues**: [Open an issue](https://github.com/Samsomyajit/windpulse/issues)
- **Documentation**: [Project website](https://samsomyajit.github.io/windpulse/)
- **Examples**: Check the `images/` directory for sample outputs

## Additional Resources

- [Methodology Documentation](docs/methodology.md)
- [Results & Analysis](docs/results.md)
- [Visualization Gallery](docs/gallery.md)
- [Contributing Guidelines](CONTRIBUTING.md)
- [Changelog](CHANGELOG.md)

---

Happy analyzing! If you find this useful, please consider starring the repository ⭐
