# ML4MSD - Homework 2

**Author:** Ardavan Mehdizadeh  
**Course:** ML4MSD  
**Due Date:** Monday, October 6, 2025, 11:59 PM

## Overview

This homework focuses on data manipulation with Pandas and implementing machine learning fundamentals from scratch, specifically ridge regression without using Scikit-Learn.

## Project Structure

```
Homework2/
├── data/                              # Dataset
│   └── band_gap_data.json            # Band gap materials data
├── notebooks/                         # Jupyter notebooks
│   ├── assignment1_filtering.ipynb   # Data filtering methods comparison
│   └── assignment2_ridge_regression.ipynb  # Ridge regression implementation
├── src/                               # Python source code (if needed)
│   └── __init__.py
├── results/                           # Output files
│   ├── figures/                      # Generated plots (png/pdf)
│   └── metrics/                      # Performance metrics
├── docs/                              # Documentation
│   └── assignment3_summary.md        # Reading summary
├── requirements.txt                   # Python dependencies
└── README.md                          # This file
```

## Setup

### Installation

```bash
# Install dependencies
pip install -r requirements.txt

# Or using uv (faster)
uv pip install -r requirements.txt
```

### Running the Notebooks

```bash
# Launch Jupyter
jupyter notebook

# Navigate to notebooks/ folder and open the desired notebook
```

## Assignments

### Assignment 1: Data Filtering Performance Comparison
- **Objective:** Compare three methods for filtering band gap data
- **Methods:** Boolean masking, for-loop with `iat`, and `iloc`
- **Filters:** `temperature_K > 50`, `crystallinity == "Polycrystalline"`, `exp_method == "Reflection"`
- **Output:** Timing comparison for all three methods

### Assignment 2: Ridge Regression from Scratch
- **Objective:** Implement ridge regression without Scikit-Learn
- **Tasks:**
  1. Data cleaning and preprocessing
  2. One-hot encoding for categorical features
  3. Pearson correlation analysis
  4. Train/test split (80/20)
  5. Ridge regression with different alpha values
  6. MSE tracking and visualization
  7. Parity plot and MSE vs. alpha plot
- **Output:** Analysis plots (saved in `results/figures/`)

### Assignment 3: Reading Summary
- **Objective:** Summarize chapters from "Machine Learning Refined"
- **Chapters:** 5.6, 6.5-6.10, 7.3-7.4, plus 1-2 chapters from 9, 10, 11, or 14
- **Output:** Summary document in `docs/assignment3_summary.md`

## Results

All figures and metrics will be saved in the `results/` folder:
- `results/figures/` - PNG/PDF plots
- `results/metrics/` - Performance metrics (CSV/JSON)

## References

- Course GitHub: [ML4MSD-Files](https://github.com/d2r2group/ML4MSD-Files)
- Homework Instructions: [hw2.md](https://github.com/d2r2group/ML4MSD-Files/blob/main/Homework/Homework2/hw2.md)
- Machine Learning Refined: [Free GitHub Link](https://github.com/neonwatty/machine-learning-refined)