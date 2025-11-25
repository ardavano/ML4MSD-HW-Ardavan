# Assignment 1 Summary - Cu DFT Analysis

**Student:** Ardavan  
**Element:** Cu (Copper)  
**Date:** November 24, 2025

## Results

- **Convergence parameters:** E_cutoff = 500 eV, k-points = 4×4×4
- **FCC structure:** a = 3.50 Å, E = -4.586 eV
- **BCC structure:** a = 2.83 Å, E = -4.619 eV
- **Experimental:** FCC with a = 3.61 Å

## Summary

DFT-LDA calculations for Cu predict a BCC ground state (a=2.83 Å, E=-4.619 eV) rather than the experimentally observed FCC structure (a=3.50 Å, E=-4.586 eV), with an energy difference of only 0.03 eV highlighting LDA's sensitivity in phase stability predictions. The calculated FCC lattice constant underestimates the experimental value (3.61 Å) by 3%, while the band structure correctly shows metallic character with no bandgap.

## Key Observations

- LDA incorrectly predicts BCC as more stable than FCC by 0.03 eV
- FCC lattice constant error: ~3% (typical for LDA)
- Band structure shows metallic character (no bandgap)