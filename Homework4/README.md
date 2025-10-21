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