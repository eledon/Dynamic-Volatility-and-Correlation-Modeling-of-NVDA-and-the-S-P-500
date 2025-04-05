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
- [Diagnostics](#diagnostics)
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

- **ADF & KPSS tests** confirmed both return series are stationary  
- **Jarque-Bera tests** rejected normality for both series  
- NVDA showed more **volatility clustering**, especially **after 2020**  
- **Rolling correlation** plots revealed changing co-movement:  
  - Relatively low/stable before 2020  
  - Marked increase and fluctuations in correlation after 2020

---

## ⚙️ Modeling

### 🔹 ACF/PACF: Model Order Selection

We used ACF and PACF plots of squared returns to guide model choice:

- NVDA showed significant lags at 1, 7, 8  
- GSPC had sustained spikes at 1, 2, 4, 6–9  
- Suggests ARCH effects over multiple lags

### 🔹 GARCH(0,5): Baseline

To test for short-term volatility clustering, we fit a **GARCH(0,5)** model:

- **ARCH LM test (lags=5)** strongly rejected the null of no ARCH  
- **Sum of α₁ to α₅**:
  - NVDA: 0.610 → moderate memory
  - GSPC: 0.789 → high persistence

### 🔹 GARCH(1,1): Main Univariate Model

Then we fit **sGARCH(1,1)** models:

- Captures both short-term shocks (α₁) and long-term memory (β₁)
- **Alpha + Beta**:
  - NVDA: 0.957
  - GSPC: 0.962

### 🔹 DCC-GARCH(1,1)

Finally, we used the univariate GARCH models as inputs to a **DCC(1,1)** model:

- Captures dynamic conditional correlation  
- **DCC Alpha + Beta = 0.742**  
- Allows modeling of time-varying dependence between the assets

---

## 📈 Forecasting

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="700"/>

We produced **100-step-ahead forecasts** of conditional **covariance and correlation** using the fitted DCC-GARCH model.

🟥 **Red vertical line** marks the start of forecast.  
🔵 **Flat forecast line**: Because DCC-GARCH is a **mean-reverting model**, it forecasts the future conditional correlation and volatility based on the current state, assuming no new information.

---

## ✅ Results

- **High Persistence**:  
  - NVDA α+β = 0.957  
  - GSPC α+β = 0.962  
- **Dynamic Correlation**:  
  - DCC α+β = 0.742  
  - Average correlation ≈ **0.57**, increasing after 2020  
- **NVDA’s risk profile changed after 2020** — more volatile and more tightly correlated with the market

---

## 🧪 Diagnostics

### 🔹 Residual Checks (GARCH)

- **Ljung-Box**: No significant autocorrelation in residuals  
- **Jarque-Bera**: Rejected normality  
- **ARCH LM**: No remaining ARCH effects after GARCH fitting  
- **Nyblom Stability Test**:  
  - GSPC model is borderline unstable (joint statistic = 8.6 > 1.6 critical)

### 🔹 🔍 Sign Bias Test

Helps detect **asymmetries** in volatility response to positive/negative returns.

- **NVDA**:  
  - All individual effects not significant  
  - Joint effect: marginally significant (p = 0.08)  
- **GSPC**:  
  - Strong significance in overall test (p < 0.001)  
  - Indicates **asymmetric volatility**, not fully captured by GARCH(1,1)

📌 Suggestion: Future modeling can consider **EGARCH or GJR-GARCH** to model asymmetric volatility.

---

## 🧾 Conclusion

This project shows how dynamic GARCH-based modeling can reveal evolving relationships between assets.

- NVDA became **increasingly correlated** with the market after 2020  
- **DCC-GARCH** provided a powerful way to model time-varying volatility and co-movement  
- **Model diagnostics** confirmed GARCH fit but pointed to asymmetries  
- Forecasting revealed stable expectations for volatility/correlation unless new shocks arrive

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full analysis  
- `S&P500_NVDA.R`: Supporting scripts  
- `readme_plots/`: Banner and forecast plots

---

📬 **Feel free to fork, clone, or star this repo!**  
Let’s explore volatility together ✨



