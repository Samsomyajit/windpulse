# Images Directory

This directory contains all visualization outputs extracted from the WindPulse analysis notebook (`meintanance_wpd.ipynb`).

## Contents

- **60 PNG images**: High-resolution visualization outputs
- **image_index.json**: Metadata file mapping images to notebook cells

## Image Categories

### Contour Heat Maps (Images 1-5)
Comprehensive contour plots showing wind speed and power density patterns across time and months for multiple locations.

- `image_001.png` - Initial setup visualization
- `image_002.png` - Multi-site contour plot (MWS & WPD)
- `image_003.png` - Wind MWS analysis at 10m hub height
- `image_004.png` - Full pipeline output (part 1)
- `image_005.png` - Full pipeline output (part 2)

### Individual Site Analysis (Images 6-41)
Detailed analysis for individual wind farm sites including:
- Monthly maintenance strips (mean-based and risk-controlled)
- Ridge plots of seasonal diurnal WPD patterns
- Risk-loss frontier curves
- Ramp rate vs. mean WPD scatter plots
- Monthly boxplots and statistical distributions

These 36 images provide comprehensive operational and analytical insights for each location.

### Multi-Site Comparison Grids (Images 42-46)
3×2 grid layouts comparing 6 wind farm sites simultaneously:

- `image_042.png` - Maintenance strips comparison grid
- `image_043.png` - Seasonal diurnal profiles grid
- `image_044.png` - Risk-loss frontiers grid
- `image_045.png` - Ramp analysis comparison grid
- `image_046.png` - Additional comparative metrics

### Enhanced Analysis (Images 47-48)
Advanced statistical visualizations:

- `image_047.png` - Enhanced resolution analysis
- `image_048.png` - Normalized comparison plots

### Clustering & Flow Analysis (Images 49-58)
Machine learning-based clustering and flow visualizations:

- `image_049.png` - Sankey/Alluvial diagram
- `image_050-052.png` - PCA clustering plots
- `image_053-055.png` - t-SNE clustering visualizations
- `image_056-058.png` - UMAP clustering results

### Seasonal Analysis (Images 59-60)
Seasonal contour plots:

- `image_059.png` - Seasonal pattern visualization
- `image_060.png` - Cross-seasonal comparison

## Image Specifications

- **Format**: PNG (Portable Network Graphics)
- **Resolution**: High resolution suitable for publication
- **Color Mode**: RGB
- **Typical Size**: 38 KB - 1.3 MB per image
- **Dimensions**: Variable, optimized for each visualization type

## Usage in Documentation

These images are referenced in the project documentation:
- **docs/gallery.md**: Complete gallery with all images
- **docs/results.md**: Key results with selected visualizations
- **GitHub Pages**: Available at the project website

## Accessing Images

### Via GitHub
Browse images directly: [github.com/Samsomyajit/windpulse/tree/main/images](https://github.com/Samsomyajit/windpulse/tree/main/images)

### Via GitHub Pages
View in the interactive gallery: [WindPulse Gallery](https://samsomyajit.github.io/windpulse/gallery.html)

### Programmatic Access
```python
import json

# Load image metadata
with open('image_index.json', 'r') as f:
    index = json.load(f)

# List all images
for img_info in index:
    print(f"{img_info['filename']} from cell {img_info['cell_idx']}")
```

## Regenerating Images

To regenerate these images from the notebook:

```bash
# Ensure dependencies are installed
pip install -r requirements.txt

# Run the notebook
jupyter nbconvert --to notebook --execute meintanance_wpd.ipynb

# Or extract images programmatically
python extract_images.py
```

## Image Metadata

The `image_index.json` file contains:
```json
[
  {
    "filename": "image_001.png",
    "cell_idx": 1,
    "output_idx": 0
  },
  ...
]
```

This metadata allows you to:
- Trace images back to source code
- Understand the analysis context
- Reproduce specific visualizations
- Automate documentation updates

## Citation

If you use these visualizations in publications, please cite:

```
WindPulse: Heat Map-Based Clustered Diurnal Wind Power Density Analysis 
for Optimized Maintenance Scheduling of Wind Farms in India
https://github.com/Samsomyajit/windpulse
```

## License

All images are part of the WindPulse project and are licensed under the MIT License. See the LICENSE file in the root directory for details.

---

For more information, see the main [README](../README.md) or visit the [documentation](../docs/index.md).
