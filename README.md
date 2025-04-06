# ✨ Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500

Modeling the time-varying volatility and conditional correlation between NVIDIA (NVDA) and the S&P 500 index using EWMA, GARCH, and DCC-GARCH models in R.

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/chris-li-6Y6OnwBKk-o-unsplash.jpg" width="600"/>

![R](https://img.shields.io/badge/R-TimeSeries-blue?logo=r)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Model](https://img.shields.io/badge/Model-GARCH%2FDCC-yellowgreen)
![Data](https://img.shields.io/badge/Data-Yahoo%20Finance-orange)

---

## 📘 Table of Contents
- [Overview](#overview)
- [Technologies](#technologies)
- [Research Question](#research-question)
- [Dataset](#dataset)
- [Exploratory Analysis](#exploratory-analysis)
- [Modeling](#modeling)
  - [EWMA (Benchmark)](#ewma-benchmark)
  - [GARCH(0,5): Baseline](#garch05-baseline)
  - [GARCH(1,1): Parsimonious](#garch11-parsimonious)
  - [DCC-GARCH(1,1): Dynamic Correlation](#dcc-garch11-dynamic-correlation)
- [Diagnostics](#diagnostics)
- [Results](#results)
- [Forecasting](#forecasting)
- [Conclusion](#conclusion)
- [Project Files](#project-files)

---

## 🗭 Overview

This project investigates how NVIDIA stock returns co-move with the S&P 500 index over time. It uses daily log returns and explores time-varying volatility through GARCH models and time-varying correlation using DCC-GARCH.

The approach builds progressively from a benchmark model (EWMA), through univariate GARCH variants, to the full multivariate DCC-GARCH specification.

---

## 🧪 Technologies
- **Language**: R  
- **Libraries**: `rugarch`, `rmgarch`, `fGarch`, `ggplot2`, `PerformanceAnalytics`, `tseries`, `zoo`, `patchwork`

---

## ❓ Research Question

> How do volatility and correlation between NVDA and the S&P 500 evolve over time?  
> Which models best capture the time-varying nature of market co-movement and risk exposure?

---

## 📊 Dataset

- **Source**: Yahoo Finance  
- **Assets**: NVIDIA (NVDA) and S&P 500 Index (^GSPC)  
- **Period**: 2013–2024 (daily)  
- **Variables**: Adjusted Closing Prices → Log Returns

---

## 🔍 Exploratory Analysis

- **Stationarity**: ADF and KPSS tests confirm that log returns are stationary
- **Distribution**: Jarque-Bera tests reject normality for both series
- **Correlation**: Rolling 60-day correlation reveals an upward trend post-2020
- **Volatility**: NVDA shows higher variance and volatility clustering
- **ACF/PACF of squared returns**:
  - NVDA: significant spikes at lags 1, 7, 8
  - GSPC: strong spikes at lags 1, 2, 4, 6–9
  → **Suggests ARCH effects** → motivates use of GARCH models

---

## ⚙️ Modeling

### 🔹 EWMA (Benchmark)
- **Purpose**: Establish a simple baseline for time-varying covariance
- **Model**: Exponential Weighted Moving Average with λ = 0.94
- **Why?**: Non-parametric, quick to compute, emphasizes recent returns
- **Usage**: Provides visual and numerical benchmark for comparison

### 🔹 GARCH(0,5): Baseline
- **Purpose**: Capture higher-order ARCH effects seen in PACF
- **Why this order?**: PACF of squared returns shows multiple lags
- **Results**:
  - NVDA: αΣ = 0.61  
  - GSPC: αΣ = 0.79
- **Limitations**: High number of parameters → lower interpretability

### 🔹 GARCH(1,1): Parsimonious
- **Purpose**: Capture volatility shocks and persistence in a compact form
- **Why this model?**: Widely used standard, easier to interpret, fewer parameters
- **Key Parameters**:
  - NVDA: α+ β = 0.957
  - GSPC: α+ β = 0.962
- **Insight**: Very persistent volatility, supports market risk modeling

### 🔹 DCC-GARCH(1,1): Dynamic Correlation
- **Purpose**: Estimate time-varying conditional correlation
- **Built from**: Two univariate GARCH(1,1) models
- **Key Coefficients**:
  - DCC α = 0.144, DCC β = 0.598 → α + β = 0.742
- **Interpretation**: Correlations are persistent but evolve dynamically

---

## 🧪 Diagnostics

### Residual Checks
- **Ljung-Box Q**: No significant autocorrelation in standardized residuals
- **ARCH-LM**: No remaining ARCH effects → GARCH(1,1) adequately captures heteroskedasticity
- **Jarque-Bera**: Residuals are non-normal (common in financial returns)

### Nyblom Stability Test
- **GSPC**: Joint Statistic = 8.63 > 1.6 critical → Suggests parameter instability

### Sign Bias Test
- Tests whether positive and negative returns affect volatility asymmetrically

| Metric             | NVDA     | GSPC     |
|--------------------|----------|----------|
| Sign Bias          | 0.158    | **0.0002** |
| Negative Sign Bias | 0.675    | 0.756    |
| Positive Sign Bias | 0.683    | 0.858    |
| **Joint Effect**   | 0.086    | **3e-5** |

- **Conclusion**:
  - NVDA: Slight asymmetry
  - GSPC: Strong asymmetry → future work should explore EGARCH

---

## ✅ Results

- **Volatility Persistence**:
  - NVDA GARCH(1,1): α+ β = **0.957**
  - GSPC GARCH(1,1): α+ β = **0.962**
- **DCC-GARCH**: Dynamic correlation evolves over time (DCC α+ β = 0.742)
- **Mean Correlation**: ~**0.57**
- **Structural Shift**: Post-2020, NVDA becomes more strongly correlated with S&P 500

---

## 📈 Forecasting

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="700"/>

We generate **100-step-ahead forecasts** for conditional covariance and correlation:
- **Red line**: Start of forecast horizon
- **Flat forecast**: DCC-GARCH assumes **no future shocks** beyond today → forecasts revert to conditional means

---

## 📅 Conclusion

This project shows how time-varying volatility and correlation models help explain evolving market dynamics:

- NVDA’s volatility is persistent and increasing post-2020
- Its correlation with the broader market has also grown
- **DCC-GARCH** effectively models these dynamics
- **Asymmetry in GSPC** implies further modeling (e.g., EGARCH) is warranted

**Applications**:
- Risk management
- Portfolio construction
- Dynamic hedging strategies

---

## 📁 Project Files
- `S&P500_vs_NVDA.Rmd`: Full analysis and report
- `S&P500_NVDA.R`: Supporting scripts
- `readme_plots/`: Banner and forecast images

---

📢 Explore, fork, or contribute. Finance is dynamic. So are the models that describe it. 🌟






