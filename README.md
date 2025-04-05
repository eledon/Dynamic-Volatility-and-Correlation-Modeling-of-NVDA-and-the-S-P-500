# ✨ Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500

Modeling the time-varying volatility and conditional correlation between NVIDIA (NVDA) and the S&P 500 index using GARCH and DCC-GARCH in R.

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/chris-li-6Y6OnwBKk-o-unsplash.jpg" width="600" height="360"/>

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
- [Model Diagnostics](#model-diagnostics)
- [Forecasting](#forecasting)
- [Results](#results)
- [Conclusion](#conclusion)

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

- ADF & KPSS tests confirm **stationarity** of log returns
- **NVDA** shows stronger volatility clustering compared to the **S&P 500**
- Rolling correlations demonstrate a **structural shift in co-movement post-2020**
- PACF and ACF plots guide the choice of model order

---

## ⚙️ Modeling

- **Univariate GARCH(1,1)** applied to NVDA and GSPC individually
- **DCC-GARCH(1,1)** captures **dynamic conditional correlation**
- Models estimated using the `rugarch` and `rmgarch` packages

---

## 🧪 Model Diagnostics

We validate model assumptions using several tests:

- **Ljung-Box Test** confirms absence of autocorrelation in standardized residuals
- **Jarque-Bera Test** indicates **non-normality**, as expected in financial returns
- **ARCH LM Test** confirms presence of ARCH effects (justifying GARCH models)
- **Sign Bias Test** detects **asymmetric effects**:
  - For NVDA, no significant sign bias (suggests symmetric model is sufficient)
  - For GSPC, **strong sign bias** detected — negative/positive shocks affect volatility differently → GARCH may be misspecified

---

## 📈 Forecasting

We produce 100-step-ahead forecasts for conditional covariance and correlation using the fitted DCC model.

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="600" height="320"/>

### 🔍 Forecast Interpretation:
- The forecasted **covariance and correlation remain nearly flat** after the red vertical line.
- This flatness occurs because **GARCH-based forecasts quickly stabilize to their unconditional levels** when no new shocks are present.

---

## ✅ Results

- **High Persistence**: NVDA α+β = 0.957, GSPC α+β = 0.962  
- **DCC α+β = 0.742** → dynamic correlations are stable but evolving  
- **Average correlation** ~0.57; rises sharply after 2020  
- **Volatility and co-movement increased significantly post-COVID**

---

## 🧾 Conclusion

- The GARCH(1,1) model captures volatility clustering in both series.
- DCC-GARCH effectively models **time-varying correlation**.
- A key insight: **NVDA became more correlated with the broader market (S&P 500) after 2020**, possibly due to its increased market cap and inclusion in major indices.
- While GARCH(1,1) suffices for NVDA, GSPC may benefit from asymmetric models.

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full analysis  
- `readme_plots/`: Forecast and banner images  
- `S&P500_NVDA.R`: Supporting scripts

---


