# AQI Analysis & Forecasting (2015–2020)

This project analyzes long-term Air Quality Index (AQI) trends across multiple Indian cities and builds a short-term forecasting model using machine learning.
The work includes complete preprocessing (missing values, outliers, temporal feature engineering), training a Random Forest model for day-ahead AQI predictions and A multi-page Power BI dashboard is included to visualize city-wise trends, pollutant distributions, seasonal patterns, and state-level insights.

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

Screenshots are placed in `/Images`.

---

## Quick results (high level)

- The model captures short-term seasonal spikes (winter peaks) and city-level differences driven primarily by PM2.5 and PM10.
- Forecasts are produced for a short horizon (example: 2020-07-02 to 2020-07-15) per city.

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


## Run the notebook (recommended)

1. Create a virtual environment and install dependencies:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

2. Open the notebook:

```bash
jupyter notebook notebook/AQI_Forecasting.ipynb
```

3. Follow the notebook cells in order. The notebook is structured so the preprocessing and feature-engineering cells run independently from the modeling cells (so you can reuse cleaned data if needed).
