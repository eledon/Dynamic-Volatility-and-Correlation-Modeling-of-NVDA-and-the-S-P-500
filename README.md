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
- [Interpretation & Practical Use](#interpretation--practical-use)
- [Conclusion](#conclusion)
- [Project Files](#project-files)

---

## 🧭 Overview

This project investigates how NVIDIA (NVDA) stock returns co-move with the S&P 500 index. Using log returns, we model conditional volatility with **univariate GARCH(1,1)** and estimate **dynamic conditional correlation** with the **DCC-GARCH** framework.

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

- **Stationarity confirmed** via ADF and KPSS tests for log returns
- **High volatility clustering** observed in NVDA compared to the S&P 500
- **Rolling correlation structure** reveals **stable moderate correlation** before 2020, followed by more volatile and higher correlations after 2020
- **ACF/PACF patterns** suggest autocorrelation in GSPC but not NVDA
- NVDA shows signs of behavior shift around 2020—possibly tied to broader tech-sector momentum or pandemic-related volatility

---

## ⚙️ Modeling

- Univariate **GARCH(1,1)** models were fitted for both NVDA and GSPC
- Joint modeling via **DCC-GARCH(1,1)** captures evolving co-movements
- Model diagnostics confirm good fit: residuals pass Ljung-Box and ARCH tests
- **Sign Bias Tests** were run to assess asymmetry and leverage effects

---

## 📈 Forecasting

<img src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" width="600"/>

### 🔮 Forecast Explanation

- The red **vertical line** separates observed data from **100-step-ahead forecasts**
- The **blue horizontal line** shows the long-term average (mean) for comparison
- The **flat line** behavior in the forecast occurs because the **DCC-GARCH model converges to a long-run conditional expectation** when no new data is available
- This is typical and expected in models where the correlation process is mean-reverting and there's no additional shock data

---

## ✅ Results

- **High volatility persistence**:  
  - NVDA: α + β = 0.957  
  - GSPC: α + β = 0.962  
- **Dynamic correlation** (DCC): α + β = 0.742  
- **Pre-2020 correlation** was stable and moderate  
- **Post-2020 correlation** surged and became more volatile  
- **Forecasts** indicate that correlation is expected to stabilize again

---

## 🧠 Interpretation & Practical Use

### 📊 Insights

- NVDA's behavior became **more correlated with the S&P 500 after 2020**, possibly due to macroeconomic or market structure changes
- The increase in correlation **implies reduced diversification benefits** when holding NVDA and the S&P 500 together
- Investors and analysts can use this modeling approach to **monitor risk exposure** and **adapt portfolio strategies** over time

### 🔧 Use Cases

- **Portfolio risk modeling**  
- **Dynamic hedging strategies**  
- **Monitoring time-varying exposure to market risk**
- Can be extended to other tech stocks or ETF constituents

---

## 🧾 Conclusion

DCC-GARCH modeling captures how assets behave **not just individually (volatility)** but **together (correlation)**. NVDA's increasing alignment with the S&P 500 after 2020 is a valuable signal for:

- Asset managers looking for diversification
- Analysts exploring market regimes and tech-sector dynamics
- Students and researchers interested in applied time series modeling

---

## 📁 Project Files

- `S&P500_vs_NVDA.Rmd`: Full analysis  
- `readme_plots/`: Forecast and banner images  
- `S&P500_NVDA.R`: Supporting scripts and functions

---

Feel free to ⭐ star, fork, or contribute!

