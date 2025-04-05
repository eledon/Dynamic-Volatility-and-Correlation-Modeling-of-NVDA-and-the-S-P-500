# ✨ Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500

Modeling the time-varying volatility and conditional correlation between NVIDIA (NVDA) and the S&P 500 index using GARCH and DCC-GARCH in R.

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
- [Forecasting](#forecasting)
- [Results](#results)
- [Sign Bias Test](#sign-bias-test)
- [Practical Insights](#practical-insights)
- [Project Files](#project-files)

---

## 🧭 Overview

This project investigates how NVIDIA stock returns co-move with the S&P 500 index. Using log returns, we model conditional volatility with **univariate GARCH(1,1)** and estimate time-varying correlation with the **DCC-GARCH model**.

---

## 🧪 Technologies

- **Language**: R  
- **Libraries**: `rugarch`, `rmgarch`, `ggplot2`, `tseries`, `zoo`, `PerformanceAnalytics`, `patchwork`

---

## ❓ Research Question

> How do volatility and correlation between NVDA and the S&P 500 evolve over time?

---

## 📊 Dataset

- **Source**: Yahoo Finance  
- **Assets**: NVDA, ^GSPC (S&P 500 Index)  
- **Period**: 2013–2024 (daily)  
- **Variable**: Adjusted closing prices → log returns

---

## 🔍 Exploratory Analysis

- **Stationarity**: Confirmed via ADF and KPSS tests  
- **Volatility Clustering**: NVDA shows higher and more persistent volatility  
- **Correlation Dynamics**: Rolling correlation is not constant — tends to rise after 2020  
- **ACF/PACF**: S&P 500 exhibits more short-term autocorrelation structure than NVDA  
- **Mean Comparison**: Returns are centered near zero, but NVDA has higher variation  

---

## ⚙️ Modeling

- **Univariate GARCH(1,1)** fit to both assets captures volatility persistence  
- **DCC-GARCH(1,1)** captures **time-varying conditional correlation**  
- Residuals diagnostics (Ljung-Box, ARCH-LM, Jarque-Bera) support model adequacy  
- NVDA α+β ≈ 0.957 and S&P 500 α+β ≈ 0.962 indicate strong volatility persistence

---

## 📈 Forecasting

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="600"/>

We produced **100-step-ahead forecasts** of conditional **covariance** and **correlation** between NVDA and the S&P 500.

🔴 The **vertical red line** separates the in-sample period from the forecast horizon.

- The flat pattern after the red line reflects how **GARCH/DCC models converge to their long-run expectations** once no new shocks are observed.
- This is expected behavior and shows model stability rather than failure.

---

## ✅ Results

- **Volatility Persistence**:
  - NVDA α + β = **0.957**
  - S&P 500 α + β = **0.962**
- **Dynamic Conditional Correlation (DCC)**: α + β = **0.742** → moderate responsiveness to past correlation shocks
- **Average Correlation**: ≈ **0.57**, increasing **post-2020**, possibly due to increased tech-market linkage
- **Forecast**: Suggests stable future volatility and correlation under current regime

---

## 📋 Sign Bias Test

The **Sign Bias Test** examines whether **positive or negative shocks** impact volatility **asymmetrically** (a common feature in financial time series).

### NVDA

| Test Type         | t-Value | p-Value | Result          |
|-------------------|---------|---------|-----------------|
| Sign Bias         | 1.41    | 0.158   | ❌ Not significant |
| Negative Sign Bias| 0.42    | 0.675   | ❌ Not significant |
| Positive Sign Bias| 0.41    | 0.683   | ❌ Not significant |
| Joint Effect      | 6.59    | 0.086   | ⚠️ Marginal (10%)  |

🔹 Interpretation: No strong evidence of asymmetric volatility response in NVDA, though the **joint effect** suggests mild nonlinearity may exist.

### S&P 500

| Test Type         | t-Value | p-Value | Result          |
|-------------------|---------|---------|-----------------|
| Sign Bias         | 3.69    | 0.00023 | ✅ Significant   |
| Negative Sign Bias| 0.31    | 0.756   | ❌ Not significant |
| Positive Sign Bias| 0.18    | 0.858   | ❌ Not significant |
| Joint Effect      | 23.55   | 0.00003 | ✅ Significant   |

🔹 Interpretation: The **S&P 500 exhibits strong asymmetric effects**, where **negative shocks** increase volatility more than positive ones — a typical leverage effect.

---

## 💡 Practical Insights

- **Volatility Modeling** allows investors to understand the risk structure of NVDA and how it responds to market shocks.
- The **correlation between NVDA and the market** (S&P 500) is **not constant** and has increased **notably after 2020** — possibly due to NVDA’s growing role in tech and AI.
- **DCC-GARCH** helps in **portfolio risk management** by modeling co-movements over time.
- The **forecast** component provides a foundation for **risk forecasting** in value-at-risk (VaR) or scenario simulation settings.

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full analysis notebook  
- `readme_plots/`: Forecast and banner images  
- `S&P500_NVDA.R`: Supporting scripts

---


