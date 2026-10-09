# GOOG Twitter Volume Forecasting using SARIMAX

## Project Overview

This project analyzes hourly Twitter volume related to Google (GOOG) and develops a short-term time-series forecasting model using SARIMAX.

The objective is to understand recurring intraday patterns in Twitter activity and forecast Twitter volume for the next 24 hours.

The analysis identifies clear daily seasonality in the hourly data. A SARIMAX model was then developed to capture short-term dependencies and the recurring 24-hour seasonal pattern.

---

## Objectives

- Analyze hourly Twitter volume for GOOG
- Explore temporal and intraday patterns
- Identify daily seasonality
- Develop a SARIMAX forecasting model
- Evaluate the model using a time-based holdout
- Generate a 24-hour forecast
- Quantify forecast uncertainty using confidence intervals

---

## Dataset

The dataset contains timestamped Twitter volume data related to Google (GOOG), representing the number of tweets observed over time.

### Key Statistics

| Metric | Value |
|---|---:|
| Mean | 20.17 |
| Standard Deviation | 15.93 |
| Minimum | 0 |
| Maximum | 156 |
| Median | 16 |
| 1st / 99th Percentile | 3 / 83.99 |

---

## Exploratory Data Analysis

The analysis examined the hourly Twitter volume series and investigated recurring patterns throughout the day.

The hourly data shows:

- Clear intraday fluctuations
- Higher activity during daytime hours
- Lower activity during overnight hours
- Occasional sharp increases associated with external events

The observed recurring pattern motivated the use of a seasonal time-series model with a **24-hour seasonal period**.

---

## Modeling Approach

### Model

**SARIMAX — Seasonal Autoregressive Integrated Moving Average with Exogenous Variables**

No exogenous variables were included in this implementation, so the forecasts are driven solely by historical Twitter volume.

### Model Configuration

**Non-seasonal order:**

```text
(p, d, q) = (3, 1, 2)

Seasonal order:
(P, D, Q, s) = (2, 1, 1, 24)

The 24-period seasonal component captures the daily seasonality observed in the hourly data.
Model Evaluation
The model was evaluated using a time-based 24-hour holdout.
The final 24 hours of the historical dataset were excluded from training and used as unseen validation data.
Performance
Metric	Result
MAE	20.5 tweets/hour
RMSE	31.3 tweets/hour
MAPE	26.6%


The forecast captured the overall level and daily pattern of Twitter activity, although sharp event-driven spikes were not captured effectively.
Forecasting
After evaluation, the SARIMAX model was refit using the full available hourly dataset.
A forecast was then generated for the next 24 hours.
The forecast includes:
- Point forecasts
- 95% confidence intervals
- Expected daily usage pattern based on historical behavior
Key Findings
- Twitter activity exhibits a clear daily seasonal pattern.
- Daytime hours generally show higher Twitter volume.
- Overnight hours generally show lower activity.
- SARIMAX successfully captures the overall level and recurring daily pattern.
- Event-driven spikes remain difficult to predict using a univariate historical-volume approach.
- Forecast uncertainty is represented using 95% confidence intervals.
Limitations
The current model does not incorporate external drivers such as:
- News events
- Market events
- Other external factors influencing Twitter activity
As a result, sudden event-driven spikes cannot be anticipated reliably using the current univariate approach.
Potential Improvements
Future improvements could include:
- Adding exogenous variables
- Incorporating event-related information
- Considering market-hour effects
- Recent-window retraining
- Comparing SARIMAX with alternative forecasting models

### Project Structure
GOOG-Twitter-Volume-Forecasting-SARIMAX/
│
├── hourly-forecast-of-goog-twitter-vol-using-sarimax.ipynb
├── Report.pdf
├── README.md
│
├── realTweets/
├── realAWSCloudwatch/
├── realAdExchange/
├── realKnownCause/
├── realTraffic/
├── artificialNoAnomaly/
└── artificialWithAnomaly/

Tools & Technologies
- Python
- Pandas
- NumPy
- Matplotlib
- Statsmodels
- SARIMAX
- Time-Series Analysis
- Statistical Forecasting
- Exploratory Data Analysis
Files
hourly-forecast-of-goog-twitter-vol-using-sarimax.ipynb
Contains the complete analysis, exploratory visualizations, model development, evaluation, and forecasting workflow.
Report.pdf
Detailed project report covering the analysis, modeling approach, evaluation results, forecasts, and limitations.
Author
Aabha Arora
Data Analytics | Python | SQL | Excel | Tableau | Machine Learning