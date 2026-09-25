# Global Weather Repository — Forecasting & Data Science Analysis

A full data science pipeline analyzing the [World Weather Repository](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository) dataset (Kaggle) — daily weather and air-quality readings for 200+ countries — to explore, understand, and forecast global weather trends.

This project was completed as a technical assessment for **[PM Accelerator](https://www.pmaccelerator.io/about-us)**.

> **PM Accelerator's Mission:** PM Accelerator makes industry-leading Product Management education and tools accessible to people from all backgrounds, leveling the playing field for future PM leaders — connecting members with industry leaders and the broader PM ecosystem, with a growing focus on AI product management. Its non-profit arm, **PMA Kids**, provides free PM education to teenagers from underserved families.

---

## Project Overview

The notebook (`weather_forecast_analysis.ipynb`) covers both the basic and advanced tiers of the assignment:

**Basic**
- Data cleaning & preprocessing (missing values, outliers, normalization)
- Exploratory Data Analysis — trends, correlations, temperature & precipitation visualizations
- A basic forecasting model, evaluated with multiple metrics, using `last_updated` for the time-series index

**Advanced**
- Advanced EDA — anomaly detection (Z-score vs. Isolation Forest)
- Multiple forecasting models compared, plus an ensemble
- Climate analysis (seasonal patterns by continent)
- Environmental impact (air quality vs. weather correlations)
- Feature importance (model-based + SHAP)
- Spatial and geographical pattern analysis (country-level geographic bubble maps, lat/long distributions)

## Methodology

1. **Cleaning** — Checked for missing values (none found in this snapshot; imputation logic included for robustness). Outliers handled with the IQR method for roughly-symmetric variables (temperature, pressure, wind, humidity) and 99.5th-percentile capping for zero-inflated/skewed variables (precipitation, gusts, particulate matter), since a standard IQR test misclassifies most non-zero readings on a zero-inflated variable. Core features standardized (z-score) for scale-sensitive steps.
2. **EDA** — Distribution plots, a correlation heatmap across weather and air-quality features, a global daily time series (temperature & precipitation), and condition/continent breakdowns.
3. **Basic forecasting** — Holt-Winters Exponential Smoothing on the global daily average temperature series (60-day holdout), evaluated with MAE, RMSE, MAPE, and R².
4. **Anomaly detection** — Z-score (>3σ) and Isolation Forest compared side by side, visualized via PCA.
5. **Multiple models + ensemble** — Engineered lag/rolling/seasonal features, then compared ARIMA, Linear Regression, Random Forest, and XGBoost, plus a simple-average ensemble, all on the same evaluation metrics.
6. **Feature importance** — Random Forest / XGBoost impurity-based importances plus SHAP values for a model-agnostic, per-prediction view.
7. **Climate, environmental, and spatial analyses** — Seasonal temperature patterns by continent, air-quality-vs-weather correlations, and country-level bubble maps (plotted by average latitude/longitude) showing temperature and PM2.5 patterns geographically.

## Key Results

- Model comparison (see notebook Section 6) shows the ensemble generally offers the best trade-off between accuracy and robustness; Linear Regression on engineered lag features was also a surprisingly strong baseline — a reminder that temperature is highly autocorrelated day-to-day, so simple models can compete with more complex ones here.
- Temperature follows the expected latitude gradient; air quality correlates more with geography/industrialization than with any single weather variable.
- The dataset spans ~2.3 years (May 2024–present), enough to show seasonal cycles clearly but too short a window for multi-decade climate-change conclusions — noted explicitly in the notebook.

## Repo Contents

| File | Description |
|---|---|
| `weather_forecast_analysis.ipynb` | Full analysis notebook, pre-executed with all outputs/charts embedded |
| `README.md` | This file |
| `REQUIREMENTS.md` / `requirements.txt` | Package versions needed to run the notebook |

> **Note:** `GlobalWeatherRepository.csv` is not included in this repo (dataset files aren't typically committed to git). Download it directly from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository) and place it in the same folder as the notebook before running.

## How to Run

```bash
conda create --prefix ./env python=3.11 -y
conda activate ./env
pip install -r requirements.txt
jupyter notebook
```

Then download `GlobalWeatherRepository.csv` from [Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository), place it in the same folder as the notebook, and run all cells (`Run > Run All Cells`).
