# GOOG Twitter Volume Forecasting using SARIMAX

> **Hourly time-series forecasting of GOOG Twitter activity using SARIMAX with 24-hour seasonality.**

## 📌 Project Overview

This project analyzes hourly Twitter volume related to **Google (GOOG)** and develops a short-term time-series forecasting model to predict Twitter activity over the next 24 hours.

The analysis begins with exploratory time-series analysis to identify temporal patterns and recurring intraday behavior. A clear daily pattern was observed, with higher activity during daytime hours and lower activity overnight.

Based on these patterns, a **SARIMAX model with a 24-hour seasonal period** was developed to capture short-term dependencies and daily seasonality.

The model was evaluated using a **time-based 24-hour holdout**, followed by refitting on the complete dataset to generate the final 24-hour forecast.

---

## 🎯 Objectives

The main objectives of this project are to:

- Analyze hourly Twitter volume for GOOG
- Explore temporal and intraday patterns
- Identify daily seasonality in Twitter activity
- Develop a SARIMAX forecasting model
- Evaluate forecasting performance on unseen data
- Generate a 24-hour ahead forecast
- Quantify forecast uncertainty using confidence intervals
- Identify limitations of a univariate forecasting approach

---

## 📊 Dataset

The project uses timestamped Twitter volume data related to **Google (GOOG)**, representing the number of tweets observed over time.

The repository also contains additional datasets from the **NAB (Numenta Anomaly Benchmark) corpus** used as part of the broader dataset collection.

### GOOG Twitter Volume — Summary Statistics

| Metric | Value |
|---|---:|
| Mean | 20.17 |
| Standard Deviation | 15.93 |
| Minimum | 0 |
| Maximum | 156 |
| 1st Percentile | 3 |
| Median | 16 |
| 99th Percentile | 83.99 |
| IQR Fence | -11.5 / 48.5 |

---

## 🔍 Exploratory Data Analysis

The hourly time series was analyzed to understand its temporal structure and recurring patterns.

### Key observations

- The series shows clear temporal structure.
- Regular intraday fluctuations are visible.
- Twitter activity tends to be higher during daytime hours.
- Activity tends to decrease during overnight hours.
- Occasional sharp spikes appear in the series.
- These spikes are likely associated with external events and are difficult to predict using historical volume alone.

The observed recurring intraday pattern provided the motivation for using a **24-hour seasonal component** in the forecasting model.

---

## 📈 Modeling Approach

### Model: SARIMAX

The forecasting model used in this project is:

**Seasonal Autoregressive Integrated Moving Average with Exogenous Variables (SARIMAX)**

Although the model is SARIMAX, **no exogenous variables were included** in this implementation. Forecasts are therefore driven entirely by historical Twitter volume.

### Model Configuration

#### Non-seasonal order

```text
(p, d, q) = (3, 1, 2)
```

This configuration was used to model short-term dependence and address non-stationarity.

#### Seasonal order

```text
(P, D, Q, s) = (2, 1, 1, 24)
```

The seasonal period of **24** represents the hourly daily cycle.

This allows the model to capture recurring daily patterns in Twitter activity.

---

## 🧪 Model Evaluation

The model was evaluated using a **time-based 24-hour holdout**.

The final 24 hours of the historical dataset were excluded from training and treated as unseen validation data.

### Evaluation Process

1. Historical hourly data was used for model training.
2. The final 24 hours were held out for validation.
3. Forecasts were generated for the unseen 24-hour period.
4. Forecasts were compared against actual Twitter volume.
5. Performance was evaluated using MAE, RMSE, and MAPE.
6. The model was subsequently refit on the full dataset for final forecasting.

---

## 📊 Model Performance

| Metric | Result |
|---|---:|
| **MAE** | **20.5 tweets/hour** |
| **RMSE** | **31.3 tweets/hour** |
| **MAPE** | **26.6%** |

### Interpretation

The model captures the **overall level and recurring daily pattern** of Twitter activity reasonably well.

However, the forecast is smoother than the actual series and does not capture sudden event-driven spikes effectively.

---

## 🔮 Forecasting

After evaluation, the SARIMAX model was refit using the complete available hourly dataset.

A **24-hour ahead forecast** was then generated.

The final forecast includes:

- Hourly point forecasts
- 95% confidence intervals
- Expected daily usage pattern based on historical behavior

The confidence intervals provide an indication of forecast uncertainty across the prediction horizon.

---

## 📌 Key Findings

### 1. Strong daily seasonality

The analysis identified a recurring 24-hour pattern in Twitter activity.

### 2. Daytime activity is generally higher

Average Twitter volume tends to increase during daytime hours and decrease overnight.

### 3. SARIMAX captures recurring patterns

The model successfully captures the general level and daily seasonal behavior of the series.

### 4. Event-driven spikes are difficult to forecast

Sudden increases in Twitter volume are not captured effectively by the model because the current implementation relies only on historical Twitter volume.

### 5. Forecast uncertainty increases across the horizon

The 95% confidence intervals illustrate the uncertainty associated with the 24-hour forecast.

---

## ⚠️ Limitations

This project uses a **univariate forecasting approach**, meaning the model relies only on historical Twitter volume.

It does not incorporate external drivers such as:

- News events
- Market events
- Other external factors that may influence Twitter activity

Because of this, sudden event-driven spikes cannot be anticipated reliably.

---

## 🚀 Potential Improvements

Future versions of the project could explore:

- Adding exogenous variables to the forecasting model
- Incorporating event-related information
- Including market-hour effects
- Retraining the model using a more recent rolling window
- Comparing SARIMAX against alternative forecasting approaches
- Evaluating additional forecasting metrics and validation windows

---

## 🛠️ Tools & Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Statsmodels**
- **SARIMAX**
- **Time-Series Analysis**
- **Statistical Forecasting**
- **Exploratory Data Analysis**

---

## 📁 Project Structure

```text
GOOG-Twitter-Volume-Forecasting-SARIMAX/
│
├── README.md
├── Report.pdf
├── hourly-forecast-of-goog-twitter-vol-using-sarimax.ipynb
│
├── realTweets/
│   └── GOOG Twitter volume data
│
├── realAWSCloudwatch/
├── realAdExchange/
├── realKnownCause/
├── realTraffic/
│
├── artificialNoAnomaly/
└── artificialWithAnomaly/
```

---

## 📓 Notebook

The main analysis and forecasting workflow is available in:

`hourly-forecast-of-goog-twitter-vol-using-sarimax.ipynb`

The notebook contains the analysis and modeling workflow used to explore the data, identify temporal patterns, build the SARIMAX model, evaluate its performance, and generate forecasts.

---

## 📄 Project Report

A detailed project report is available in:

`Report.pdf`

The report contains:

- Data overview
- Exploratory visualizations
- Hour-of-day analysis
- Modeling approach
- Model evaluation
- Forecast accuracy
- Final test forecast
- 24-hour forecast
- Model limitations and potential improvements

---

## 📈 Forecasting Workflow

```text
Raw Twitter Volume Data
          │
          ▼
   Data Preparation
          │
          ▼
 Exploratory Analysis
          │
          ▼
 Identify Daily Seasonality
          │
          ▼
    SARIMAX Modeling
          │
          ▼
  24-Hour Holdout Test
          │
          ▼
 Model Evaluation
(MAE / RMSE / MAPE)
          │
          ▼
 Refit on Full Dataset
          │
          ▼
   Next 24-Hour Forecast
          │
          ▼
 Point Forecast + 95% CI
```

---

## 💡 Business / Analytical Relevance

Time-series forecasting can help organizations anticipate changes in activity levels and plan resources around expected demand.

In this project, forecasting Twitter volume provides an example of how historical behavioral patterns can be used to estimate near-term social-media activity while also highlighting the challenges created by unpredictable external events.

---

## 👩‍💻 Author

**Aabha Arora**

Aspiring Data Analyst | Python | SQL | Excel | Tableau | Machine Learning

---

## 🔗 Repository

[GOOG Twitter Volume Forecasting using SARIMAX](https://github.com/Aabha0503/GOOG-Twitter-Volume-Forecasting-SARIMAX)
