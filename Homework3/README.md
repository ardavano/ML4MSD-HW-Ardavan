**Author:** Ardavan Mehdizadeh  
**Due:** Monday, October 13, 2025

## Setup Instructions

### 1. Install Dependencies
```bash
pip install pymatgen mp-api pandas matplotlib seaborn
```

### 2. Configure Materials Project API Key

**IMPORTANT:** You need a Materials Project API key to run Assignment 2.

1. Get your API key from: https://next-gen.materialsproject.org/api
2. Copy `config_template.py` to `config.py`:
```bash
   cp config_template.py config.py
```
3. Edit `config.py` and replace `YOUR_API_KEY_HERE` with your actual API key
4. **Never commit `config.py` to Git!** (It's already in .gitignore)

### 3. Run the Notebooks
```bash
cd notebooks
jupyter notebook
```

## Project Structure
```
Homework3/
├── notebooks/
│   ├── assignment1_perovskites.ipynb
│   └── assignment2_mp_queries.ipynb
├── cif_files/
│   ├── BaTiO3_cubic.cif
│   └── BaTiO3_tetragonal_c1.3.cif
├── data/
│   └── mp_hw_data.csv
├── config_template.py        # Template - commit to Git
├── config.py                  # Your actual key - DO NOT commit!
└── .gitignore
```

## Assignments

1. **Assignment 1:** Generate perovskite structures using Pymatgen
2. **Assignment 2:** Query Materials Project API and analyze band gaps
3. **Assignment 3:** Read and annotate research papers
4. **Assignment 4:** Analyze Pymatgen OOP concepts

## Note to Grader

To run Assignment 2, you'll need to:
1. Create `config.py` from `config_template.py`
2. Add your own Materials Project API key

Alternatively, the results are saved in `data/mp_hw_data.csv` and can be loaded directly.