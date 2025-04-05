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
- [Diagnostics](#diagnostics)
- [Results](#results)
- [Forecasting](#forecasting)
- [Conclusion](#conclusion)
- [Files](#project-files)

---

## 🧭 Overview

This project investigates how NVIDIA stock returns co-move with the S&P 500 index. Using log returns, we model conditional volatility with **univariate GARCH** and estimate time-varying correlation with the **DCC-GARCH model**.

---

## 🧪 Technologies

- **Language**: R  
- **Libraries**: `rugarch`, `rmgarch`, `fGarch`, `ggplot2`, `tseries`, `zoo`, `PerformanceAnalytics`, `patchwork`

---

## ❓ Research Question

> How do volatility and correlation between NVDA and the S&P 500 evolve over time?  
> What is the magnitude and persistence of volatility shocks and co-movement?

---

## 📊 Dataset

- **Source**: Yahoo Finance  
- **Assets**: NVDA, ^GSPC (S&P 500 Index)  
- **Period**: 2013–2024 (daily)  
- **Variable**: Adjusted closing prices → log returns

---

## 🔍 Exploratory Analysis

- **ADF & KPSS tests** confirm both return series are stationary  
- **Jarque-Bera tests** reject normality  
- **Rolling correlation** shows rising correlation after 2020  
- **NVDA** becomes more volatile and market-coupled in recent years  
- **ACF/PACF** of squared returns indicate presence of ARCH effects:
  - NVDA: significant at lags 1, 7, 8  
  - GSPC: strong spikes at lags 1, 2, 4, 6–9  
  → Suggest using GARCH-type models

---

## ⚙️ Modeling

### 🔹 GARCH(0,5): Baseline

We begin with a **GARCH(0,5)** model to capture short-term memory in volatility. ARCH LM tests confirm the presence of conditional heteroskedasticity. The sum of ARCH coefficients:

- NVDA: **0.610**
- GSPC: **0.789**

This suggests high persistence in volatility shocks.

### 🔹 GARCH(1,1): Simpler and More Interpretable

We switch to **GARCH(1,1)** for parsimony and broader comparability. It captures both short-term shocks (α₁) and long-term persistence (β₁). The model performs well in capturing volatility clustering.

### 🔹 DCC-GARCH(1,1): Modeling Co-Movement

Using the fitted univariate GARCH(1,1) models, we estimate a **DCC-GARCH(1,1)** to model dynamic conditional correlation between NVDA and the S&P 500.

---

## 🧪 Diagnostics

### 🔹 Residual Checks

- **Ljung-Box (Q)**: No autocorrelation in standardized residuals  
- **ARCH-LM**: No remaining ARCH effects after GARCH fit  
- **Jarque-Bera**: Residuals remain non-normal  
- **Nyblom Stability Test**:
  - GSPC borderline unstable (Joint Stat = 8.63 > 1.6 critical)

### 🔹 Sign Bias Test

Used to detect **volatility asymmetry**:

| Metric                 | NVDA        | GSPC        |
|------------------------|-------------|-------------|
| Sign Bias              | p = 0.158   | p = 0.0002  |
| Negative Sign Bias     | p = 0.675   | p = 0.756   |
| Positive Sign Bias     | p = 0.683   | p = 0.858   |
| **Joint Effect**       | **p = 0.086** | **p = 3e-5** |

- **NVDA**: marginal asymmetry  
- **GSPC**: strong asymmetry → consider EGARCH/GJR in future work

---

## ✅ Results

- **Persistence**:  
  - NVDA α+β = **0.957**  
  - GSPC α+β = **0.962**  
- **DCC α+β = 0.742** → dynamic correlations evolve but are moderately persistent  
- **Avg correlation ≈ 0.57**, trending upward post-2020  
- NVDA has become more market-coupled in recent years

---

## 📈 Forecasting

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="700"/>

We produced **100-step-ahead forecasts** of conditional covariance and correlation between NVDA and GSPC using the DCC-GARCH model.

🟥 **Red line** marks the start of the forecast horizon  
🟦 **Flat lines** occur because **DCC-GARCH assumes no new shocks** beyond the current state, so forecasts revert to conditional means

---

## 🧾 Conclusion

DCC-GARCH is an effective tool to study how asset volatility and correlation evolve over time.

- NVDA has become **increasingly correlated** with the S&P 500 since 2020  
- DCC-GARCH reveals **time-varying market exposure**  
- While GARCH(1,1) models volatility well, diagnostics suggest asymmetry → future work could explore **EGARCH**  
- This framework can support **risk management**, **portfolio optimization**, or **hedging strategies**

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full report and analysis  
- `S&P500_NVDA.R`: Support scripts  
- `readme_plots/`: Banner and forecast plot

---

📬 **Explore, fork, or contribute to this repo. Insights await in volatility.** 📉✨




