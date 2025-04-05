# Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500
A comprehensive time series analysis of NVDA and S&amp;P 500 returns. Focuses on testing for ARCH effects, fitting GARCH(1,1) models, and estimating conditional covariances and correlations using DCC-GARCH frameworks.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>✨ Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      margin: 40px;
      max-width: 900px;
    }
    h1, h2, h3 {
      color: #2c3e50;
    }
    .badge {
      display: inline-block;
      margin: 4px 4px 10px 0;
    }
    img.banner {
      width: 100%;
      max-width: 700px;
      height: auto;
    }
    .section {
      margin-top: 40px;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 4px;
      border-radius: 4px;
    }
  </style>
</head>
<body>

<h1>🌟 Dynamic Volatility and Correlation Modeling of NVDA and the S&P 500</h1>

<p>Modeling the time-varying volatility and conditional correlation between NVIDIA (NVDA) and the S&P 500 index using GARCH and DCC-GARCH in R.</p>

<img class="banner" src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/chris-li-6Y6OnwBKk-o-unsplash.jpg" alt="Banner Image">

<p class="badge"><img src="https://img.shields.io/badge/R-GARCH%2FDCC--GARCH-blue?logo=r"></p>
<p class="badge"><img src="https://img.shields.io/badge/Status-Completed-brightgreen"></p>
<p class="badge"><img src="https://img.shields.io/badge/Data-Yahoo%20Finance-orange"></p>

<div class="section">
<h2>📃 Table of Contents</h2>
<ul>
  <li><a href="#overview">Overview</a></li>
  <li><a href="#technologies">Technologies</a></li>
  <li><a href="#research-question">Research Question</a></li>
  <li><a href="#data">Data</a></li>
  <li><a href="#eda">Exploratory Data Analysis</a></li>
  <li><a href="#modeling">Modeling</a></li>
  <li><a href="#forecasting">Forecasting</a></li>
  <li><a href="#results">Results</a></li>
</ul>
</div>

<div class="section" id="overview">
<h2>🔍 Overview</h2>
<p>This project uses GARCH and DCC-GARCH models to examine the changing relationship between NVDA and the S&P 500. We estimate volatility for each asset and model their dynamic conditional correlation using daily returns from 2013 to 2024.</p>
</div>

<div class="section" id="technologies">
<h2>🧪 Technologies</h2>
<ul>
  <li><strong>Language:</strong> R</li>
  <li><strong>Libraries:</strong> <code>rugarch</code>, <code>rmgarch</code>, <code>zoo</code>, <code>xts</code>, <code>quantmod</code>, <code>ggplot2</code>, <code>PerformanceAnalytics</code></li>
</ul>
</div>

<div class="section" id="research-question">
<h2>❓ Research Question</h2>
<p><strong>How does the volatility of NVDA and the S&P 500 evolve over time, and how do their conditional correlations change during periods of market stress?</strong></p>
</div>

<div class="section" id="data">
<h2>📊 Data</h2>
<ul>
  <li><strong>Source:</strong> Yahoo Finance</li>
  <li><strong>Assets:</strong> NVDA and ^GSPC (S&P 500)</li>
  <li><strong>Period:</strong> January 2013 – December 2024</li>
  <li><strong>Frequency:</strong> Daily adjusted close prices</li>
</ul>
</div>

<div class="section" id="eda">
<h2>📊 Exploratory Data Analysis</h2>
<p>We compute log returns, test for stationarity, check for autocorrelation and ARCH effects, and visualize rolling covariances and correlations over time.</p>
<p><strong>Highlights:</strong></p>
<ul>
  <li>NVDA is more volatile and responsive to market changes than the S&P 500.</li>
  <li>Autocorrelation is low, but squared returns show ARCH effects, motivating GARCH modeling.</li>
</ul>
</div>

<div class="section" id="modeling">
<h2>⚖️ Modeling</h2>
<p>We fit univariate GARCH(1,1) models for NVDA and GSPC and then a DCC-GARCH(1,1) model to capture their joint dynamics.</p>
<p><strong>Key Model Outputs:</strong></p>
<ul>
  <li><strong>Alpha + Beta (NVDA):</strong> 0.957</li>
  <li><strong>Alpha + Beta (GSPC):</strong> 0.962</li>
  <li><strong>DCC Alpha + Beta:</strong> 0.742</li>
</ul>
<p>These results suggest persistent volatility and meaningful time-varying correlation.</p>
</div>

<div class="section" id="forecasting">
<h2>⏳ Forecasting</h2>
<p>We forecast 100 days ahead for both the conditional covariance and correlation between NVDA and GSPC.</p>
<img class="banner" src="https://github.com/eledon/Dynamic-Volatility-and-Correlation-Modeling-of-NVDA-and-the-S-P-500/blob/main/readme_plots/DCC_GARCH_forecast.jpg" alt="Forecast Plot">
</div>

<div class="section" id="results">
<h2>📊 Results</h2>
<ul>
  <li>Volatility and correlation increased significantly during market turbulence.</li>
  <li>DCC-GARCH captured the shifts in dependency structure well, particularly post-2020.</li>
  <li>The forecast shows expected mean reversion in correlation near its long-run average (~0.57).</li>
</ul>

<p><strong>✅ Conclusion:</strong> This project demonstrates the usefulness of DCC-GARCH in modeling co-movement between assets. NVDA, a high-beta stock, shows dynamic relationships with the broader market, making it essential for volatility forecasting and portfolio risk analysis.</p>
</div>

</body>
</html>
