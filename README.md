# ✨ Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500

Modeling the time-varying volatility and conditional correlation between NVIDIA (NVDA) and the S&P 500 index using GARCH and DCC-GARCH in R.

![Banner](https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/chris-li-6Y6OnwBKk-o-unsplash.jpg)

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

- ADF & KPSS tests confirm log returns are stationary  
- NVDA exhibits higher variance and volatility clustering  
- Rolling correlations reveal changing dependence structure  

---

## ⚙️ Modeling

- **Univariate GARCH(1,1)** fit for both NVDA and GSPC  
- **DCC-GARCH(1,1)** captures dynamic correlation  
- Residual diagnostics: Jarque-Bera, Ljung-Box, Sign Bias tests  

---

## 📈 Forecasting

![Forecast Plot](https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg)

We produce 100-step-ahead forecasts for conditional covariance and correlation between NVDA and GSPC.

---

## ✅ Results

- **High Persistence**: NVDA α+β = 0.957, GSPC α+β = 0.962  
- **DCC α+β = 0.742** → dynamic correlations are stable but evolve  
- **Average correlation** ~0.57; increases sharply post-2020  
- Forecasted correlation stabilizes after a brief increase

---

## 🧾 Conclusion

DCC-GARCH is an effective tool to capture the evolving relationship between NVDA and market movements. This project showcases how financial time series modeling provides deeper insight into asset risk and co-movement.

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full analysis  
- `readme_plots/`: Forecast and banner images  
- `S&P500_NVDA.R`: Supporting scripts

---

Feel free to explore, fork, or contribute!
