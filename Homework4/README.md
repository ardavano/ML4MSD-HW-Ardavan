# Homework 4: Assignment 1 - Exercise 11.1

Complete ML pipeline for predicting exfoliation energy of 2D materials.

## Dataset
**matbench_jdft2d** - 636 2D materials, exfoliation energy (meV/atom)

## Why This Dataset?
Exfoliation energy directly relates to surface formation and cleavage energy - core to my research on surface stability predictions using MLIPs.

## Featurization Approaches
1. **Compositional**: ElementProperty (Magpie) - 99 features
2. **Structural**: EwaldSumMatrix - 22 features

## Results

| Approach | Test MAE (meV/atom) | Test R² |
|----------|---------------------|---------|
| Compositional (Magpie) | 46.87 | 0.68 |
| Structural (EwaldSum) | 64.90 | 0.46 |
| Baseline (Mean) | 57.96 | - |

**Winner**: Compositional features - chemical identity matters more than geometry for interlayer bonding.

## Run
```bash
cd Homework4
jupyter notebook hw4_assignment1.ipynb
```

## Google Sheet Submission
Results have been submitted to the ML4MSD - Homework 4 Google Sheet.



## Assignment 2: Materials Project API + DScribe Pipeline

### Query Strategy
- **API**: Materials Project
- **Final query filters**:
  - Band gap: 1.5-2.5 eV (narrowed from 0.5-3.0 to get manageable dataset)
  - Energy above hull: < 0.01 eV/atom (very stable materials)
  - Number of elements: 2-3 (binary and ternary)
  - Number of sites: < 30 (smaller unit cells)
- **Dataset size**: 1,386 materials
- **Target**: Band gap (eV)

### Featurization
- **Method**: SOAP (Smooth Overlap of Atomic Positions) from DScribe
- **Parameters**: r_cut=6.0 Å, n_max=6, l_max=4, averaging=outer
- **Feature reduction**: 621,255 → 5,000 (variance-based selection)

### Results
- **Test MAE**: 0.2308 eV
- **Test RMSE**: 0.2747 eV
- **Test R²**: 0.1329
- **Baseline MAE**: 0.2342 eV

**Note**: Modest R² is expected for band gap prediction in narrow range (1.5-2.5 eV). Band gap is challenging to predict from structure alone without electronic structure calculations.

### Files Generated
- `parity_plots_mp_bandgap.png` - Model performance visualization
- `mp_bandgap_distribution.png` - Target distribution
- `mp_ml_pipeline_summary.csv` - Performance metrics summary

## Assignment 3: Paper Summary

### Paper
Musil et al., "Machine learning for the structure–energy relationship in atomic clusters"  
*Chemical Reviews* (2021) - Review of Descriptors  
Pages 1-6 reviewed

### Key Insights

Four main takeaways from the paper that enhanced lecture understanding:

1. **Completeness**: Importance of descriptors that map distinct structures to distinct features
2. **Trade-offs**: Why multiple descriptor types exist (speed vs accuracy vs completeness)
3. **Historical evolution**: From molecule-specific PES → transferable features → learned representations
4. **Smoothness**: Need for smooth derivatives, not just smooth values, for force predictions

### Connection to Research
These concepts directly inform descriptor selection for surface energy MLIP development.

### File
- `assignment3_paper_summary.md` - Detailed summary and analysis