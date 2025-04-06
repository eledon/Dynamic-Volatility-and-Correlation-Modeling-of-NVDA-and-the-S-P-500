# ✨ Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500

Modeling time-varying volatility and correlation between NVIDIA (NVDA) and the S&P 500 index using GARCH-family and EWMA models in **R**.

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/chris-li-6Y6OnwBKk-o-unsplash.jpg" width="600"/>

![R](https://img.shields.io/badge/R-TimeSeries-blue?logo=r)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Model](https://img.shields.io/badge/Model-GARCH%2FDCC%2FEWMA-yellowgreen)
![Data](https://img.shields.io/badge/Data-Yahoo%20Finance-orange)

---

## 📘 Table of Contents

- [Overview](#overview)
- [Technologies](#technologies)
- [Research Question](#research-question)
- [Dataset](#dataset)
- [Exploratory Analysis](#exploratory-analysis)
- [Modeling](#modeling)
  - [GARCH(0,5)](#garch05-baseline)
  - [GARCH(1,1)](#garch11-parsimonious-model)
  - [DCC-GARCH(1,1)](#dcc-garch11-dynamic-correlation)
  - [EWMA](#ewma-comparison-model)
- [Forecasting](#forecasting)
- [Conclusion](#conclusion)
- [Files](#project-files)

---

## 🧭 Overview

This project explores how NVIDIA’s stock returns relate to broader market movements by modeling volatility and correlation over time. We use log returns, GARCH-type models, and the DCC framework to assess volatility clustering, persistence, and dynamic co-movement between NVDA and the S&P 500.

---

## 🧪 Technologies

- **Language**: R  
- **Libraries**: `rugarch`, `rmgarch`, `fGarch`, `FinTS`, `ggplot2`, `tseries`, `zoo`, `patchwork`, `PerformanceAnalytics`

---

## ❓ Research Question

> How do volatility and correlation between NVDA and the S&P 500 evolve over time?
> 
> What model best captures these dynamics, and how persistent are volatility shocks and co-movements?

---

## 📊 Dataset

- **Source**: Yahoo Finance  
- **Assets**: NVIDIA (NVDA), S&P 500 Index (^GSPC)  
- **Period**: 2013–2024  
- **Frequency**: Daily  
- **Variable**: Adjusted Closing Prices → Log Returns  

---

## 🔍 Exploratory Analysis

- **Stationarity**: ADF and KPSS confirm stationarity of both return series
- **Normality**: Jarque-Bera tests reject normality for both
- **Autocorrelation**: ACF/PACF plots of squared returns suggest ARCH effects:
  - NVDA: spikes at lags 1, 7, 8  
  - GSPC: spikes at lags 1–2, 4, 6–9
- **ARCH LM Tests**: Significant for both assets (p < 0.001)
- **Rolling Correlation**: Notable rise in correlation post-2020 — stronger market dependence

---

## ⚙️ Modeling

### 🔹 GARCH(0,5): Baseline

A high-order ARCH model is used as a starting point. Total ARCH effects:

- **NVDA**: α₁+…+α₅ = 0.610  
- **GSPC**: α₁+…+α₅ = 0.789  

✅ Captures volatility clustering  
❌ Lacks a GARCH term for persistence  
❌ Many parameters → less interpretable

**Diagnostics**:
- Residuals: no significant autocorrelation or remaining ARCH  
- Normality: still rejected (JB test)

---

### 🔹 GARCH(1,1): Parsimonious Model

We switch to GARCH(1,1) for simplicity and generalizability.

- **NVDA**: α + β = 0.957  
- **GSPC**: α + β = 0.962

✅ Captures both short- and long-term volatility  
✅ Residuals pass Ljung-Box and ARCH-LM  
❌ Residuals still not normal  
❌ GSPC: **Nyblom Test** indicates parameter instability

**Sign Bias Test**:

|                  | NVDA      | GSPC       |
|------------------|-----------|------------|
| Sign Bias        | p = 0.158 | p = 0.0002 |
| Joint Effect     | p = 0.086 | p < 0.001  |

→ Suggests **volatility asymmetry** for GSPC → EGARCH could be better.

---

### 🔹 DCC-GARCH(1,1): Dynamic Correlation

A multivariate DCC-GARCH(1,1) model builds on the fitted univariate models.

- **Average Correlation**: ≈ 0.57  
- **DCC α + β**: 0.742 → correlation is persistent but mean-reverting  
- **Post-2020**: correlation rises, showing tighter market linkage

✅ Captures time-varying co-movement  
✅ Residuals stable  
✅ Enables conditional forecast of correlation

---

### 🔹 EWMA: Comparison Model

We apply an **Exponentially Weighted Moving Average (EWMA)** to returns:

- **λ = 0.94**, consistent with RiskMetrics  
- Covariance and correlation are smoother  
- Mean correlation ≈ 0.58  
- Similar post-2020 increase observed

✅ Non-parametric baseline  
✅ Easier to implement  
❌ No probabilistic interpretation  
❌ No forecasting beyond current values

---

## 📈 Forecasting

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="600"/>

**100-step-ahead forecasts** of conditional covariance and correlation using DCC-GARCH(1,1):

- 🔴 **Red line** = start of forecast horizon  
- 🔵 **Flat forecast**: DCC-GARCH assumes no new information → forecasts revert to conditional mean  
- Useful for short-term risk/portfolio forecasting

---

## 🧾 Conclusion

- NVDA has become **more correlated** with the S&P 500 post-2020  
- **GARCH(1,1)** fits volatility clustering well, but GSPC may need EGARCH  
- **DCC-GARCH(1,1)** effectively models evolving market co-movement  
- **EWMA** offers a useful benchmark  
- This framework can inform **portfolio risk, dynamic hedging, and beta estimation**

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full R Markdown notebook  
- `S&P500_NVDA.R`: Supporting script  
- `readme_plots/`: Forecast and banner images

---

📬 *Project last updated: April 5, 2025 — Contributions welcome!* 📉✨
