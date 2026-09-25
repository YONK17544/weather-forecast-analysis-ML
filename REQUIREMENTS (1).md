# Requirements

This project was built and tested with the package versions below.

## Core Data Handling
- `pandas==3.0.2`
- `numpy==2.4.4`

## Visualization
- `matplotlib==3.10.8`
- `seaborn==0.13.2`

## Machine Learning
- `scikit-learn==1.8.0`
- `xgboost==3.4.1`
- `shap==0.52.0`

## Time Series Forecasting
- `statsmodels==0.15.0`

## Geography / Country-Continent Mapping
- `country_converter`

## Notebook Support
- `jupyter`
- `nbformat==5.11.1`

## Installation

With your conda environment active, run:

```bash
conda install -y jupyter pandas numpy matplotlib seaborn scikit-learn statsmodels -c conda-forge
pip install xgboost shap country_converter nbformat
```

Or, if you'd rather use a plain `requirements.txt` with pip:

```bash
pip install -r requirements.txt
```
