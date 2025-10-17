# Day-Ahead Electricity Price Prediction

Forecasting **day-ahead hourly electricity prices** using machine learning and LSTM deep learning.  
Includes robust **EDA**, **feature engineering**, **time-based splits**, and **full evaluation** on realistic holdout years.

---

## Table of Contents
1. [Project Overview](#project-overview)  
2. [Data Sources](#data-sources)  
3. [EDA & Feature Engineering](#eda--feature-engineering)  
4. [Modeling Approach](#modeling-approach)  
5. [Training and Evaluation](#training-and-evaluation)  
6. [Results](#results)  


---

## Project Overview
This project forecasts **day-ahead electricity prices** for hourly markets using historical price, demand, and renewables supply features.  

- **Time-based splits prevent leakage**:
  - **Train:** All data before 2023  
  - **Validation:** All data from 2023  
  - **Test:** All data from 2024  

- **Goal:** Predict hourly day-ahead prices at auction time using only **available historical prices and forecasts**.

---


---

## EDA & Feature Engineering
- Statistical exploration, seasonality plots, and autocorrelation analysis  
- Created **lagged features** (e.g., `price_lag24`, `price_lag168`)  
- Rolling window features (mean, std) for prices and net load  
- Calendar features: holidays, weekends  
- **NaN handling:** All missing values removed to ensure clean model input  

---

## Modeling Approach
### Baselines
- **Naive persistence:** Yesterday's prices  
- **RandomForestRegressor:** Hour-wise regression baseline  
- **RandomForestRegressor with cross-validation:** Hour-wise regression baseline


### LSTM Deep Learning
- **Input:** Past 168 hours (7 days) of features + forecast for target hour  
- **Output:** Predicts **next 24 hours** (one day) at once or **one-step per hour**  
- **Training:** Only on historical data, validated/tested on strictly unseen future blocks  

---

## Training and Evaluation
- **Splits by calendar year** (train, validation, test)  
- **Evaluation metrics:** MAE, RMSE, R²  
- **Visualization:** Hourly predicted vs. true prices for first two weeks of the test year  

---

## Results

| Model   | Test MAE | Test MSE | Test R² |
|---------|----------|-----------|---------|
| Naive   | 29.95    | 4525.20   | 0.088   |
| RF      | 22.97    | 2503.69   | 0.398   |
| RF +CV  | 16.95    | 2103.63   | 0.501   |
| LSTM    |  18.70   |           | 0.4430   |




