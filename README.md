# AQI Analysis & Forecasting (2015–2020)

This repository contains a reproducible pipeline for analyzing Air Quality Index (AQI) data from 2015–2020 across multiple Indian cities, and a short-term forecasting model built on top of engineered temporal features. A Power BI dashboard is included for interactive exploratory analysis and visual storytelling.

---

## Project overview

The objective is straightforward: analyze historical AQI patterns, identify key insights at city and state level, and build a short-term forecasting model to predict near-future AQI using lag features and seasonal encodings. The work is split into two complementary parts:

- **Data processing & modeling** (Jupyter notebook / Python) — reproducible preprocessing, feature engineering, model training, forecasting, and evaluation.
- **Exploratory analysis & presentation** (Power BI) — interactive visuals, trends, pollutant comparisons, and maps for clear insights.

---

## Key steps performed (notebook)

1. **Data loading** — read raw dataset, parse dates, basic sanity checks.
2. **Missing value handling** — imputation or removal where appropriate, with brief justification.
3. **Outlier detection & treatment** — IQR/domain-based checks to remove extreme sensor noise.
4. **Feature engineering** —
   - `Month`, `Day`, `DayOfWeek`, `Is_Weekend` (calendar features)
   - `Sin_Day`, `Cos_Day` (seasonal encoding using day-of-year)
   - `AQI_Lag1` (previous-day AQI)
   - `AQI_Avg7` (7-day rolling mean, lagged)
5. **Modeling** — Random Forest Regressor trained on historical windows (details in notebook).
6. **Forecasting** — short-term forecasts generated per city and appended back to the dataset for comparison.
7. **Evaluation** — compute MAE and/or RMSE and produce an Actual vs Predicted plot.

---

## Power BI Dashboard (summary)

The dashboard contains multiple pages with interactive filters (Year, AQI Status, City). Main visuals include:

- Full-period AQI trend (Actual vs Forecast) — time-series line chart
- Most / Least polluted cities — ranked bar charts
- AQI level distribution and average AQI by level — pie charts
- City-wise AQI line/rank chart
- Top 10 cities by pollutant (PM2.5, PM10, NO2, SO2, O3, NH3)
- State-level pollutant totals (bar charts)
- Choropleth map of average AQI by state

Screenshots are placed in `/images/dashboard_screenshots/`.

---

## Quick results (high level)

- The model captures short-term seasonal spikes (winter peaks) and city-level differences driven primarily by PM2.5 and PM10.
- Forecasts are produced for a short horizon (example: 2020-07-02 to 2020-07-15) per city.
- Training and evaluation details (periods, error metrics) are documented in the notebook.

> **Note:** Detailed numeric results (MAE/RMSE, per-city tables, sample forecasts) are available in the Jupyter notebook.

---

## Repository structure

```
AQI-Forecasting-Project/

├── notebook/
│   └── aqi_forecasting.ipynb        # preprocessing, model training, forecasting, evaluation

├── powerbi/
│   └── AQI_Dashboard.pbix            # Power BI file (screenshots in images/)

├── data/
│   ├── raw/                          # source/raw CSVs (optional: keep out of repo if large)
│   └── cleaned/                      # cleaned datasets used by notebook

├── images/
│   └── dashboard_screenshots/        # screenshots used in README

├── src/                              # optional: helper modules (model saving, utils)

├── README.md                          # this file
└── requirements.txt                   # Python dependencies
```

---

## Run the notebook (recommended)

1. Create a virtual environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate   # or .venv\Scripts\activate on Windows
pip install -r requirements.txt
```

2. Open the notebook:

```bash
jupyter notebook notebook/aqi_forecasting.ipynb
```

3. Follow the notebook cells in order. The notebook is structured so the preprocessing and feature-engineering cells run independently from the modeling cells (so you can reuse cleaned data if needed).

---

## Notes on reproducibility and data

- If the raw dataset is large or contains restricted fields, include an anonymized sample in `data/sample/` and provide instructions on where to obtain the full data (source link).
- Keep column types and date parsing explicit in the notebook to avoid timezone/dtype issues.

---

## Limitations

- Forecasting horizon is short and the model is not intended for long-term forecasting without retraining and more features (weather, emissions, policy events).
- Data quality depends on sensor networks; some stations may have missing or noisy readings.

---

## Future scope

- Add meteorological data (temperature, humidity, wind) to improve predictions.
- Try time-series specific models (SARIMA, Prophet, LSTM) for comparative performance.
- Deploy forecasts via a minimal API (Flask/FastAPI) and refresh the Power BI report via a scheduled dataset.

---

## Tools & libraries

- Python: pandas, numpy, scikit-learn, matplotlib
- Power BI Desktop
- Jupyter Notebook

---

## Contact

If you want the README tailored further (shorter/longer, different tone), or want the notebook cleaned up into runnable scripts, tell me which format you prefer (full notebook, export to `.py`, or packaged module).
