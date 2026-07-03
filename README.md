# Risk, Correlation & Hedging — Portfolio Analysis

This repository contains a comprehensive data-driven study of risk, rolling correlation, and hedging strategies across various asset classes, including equities (S&P 500 / SPY), leveraged inverse ETFs (SDS), Treasury Bills (T-Bills), Gold, Commodities, and the US Dollar (UUP).

The analysis is implemented in a Jupyter notebook (`solutions.ipynb`) and answers 17 analytical questions regarding modern portfolio theory, minimum-variance allocations, beta calculations, hedging efficiency, and long-term portfolio growth comparisons.

---

## 📊 Dataset Overview

The project utilizes several CSV data files covering daily, weekly, and monthly frequencies:

| File Name | Frequency | Description |
| :--- | :--- | :--- |
| [`daily_prices_SPY_SDS_SSO.csv`](file:///c:/Users/User/Desktop/Projects/daily-returns/daily_prices_SPY_SDS_SSO.csv) | Daily | Price data for SPY (S&P 500 ETF), SDS (UltraShort / 2x Inverse S&P 500 ETF), and SSO (UltraPro / 2x Leveraged S&P 500 ETF). |
| [`daily_yield_irx.csv`](file:///c:/Users/User/Desktop/Projects/daily-returns/daily_yield_irx.csv) | Daily | 13-week Treasury Bill annualized yields (`^IRX`), expressed as decimals. |
| [`sp_gold_commodities_usd.csv`](file:///c:/Users/User/Desktop/Projects/daily-returns/sp_gold_commodities_usd.csv) | Monthly | Monthly returns for S&P 500, Gold, Commodities, and US Dollar (UUP). |
| [`sp_bonds_gold_commodities_US$_weekly_px.csv`](file:///c:/Users/User/Desktop/Projects/daily-returns/sp_bonds_gold_commodities_US$_weekly_px.csv) | Weekly | Weekly price data used for calculating rolling correlations and identifying market regimes. |

---

## 🔍 Key Findings & Analysis Summary

### 1. SPY / SDS & Risk-Free Comparison (Questions 1–4)
* **Zero-Risk Portfolio Weights**: Under the assumption of perfect negative correlation ($\rho = -1$), the portfolio variance is a perfect square. The risk is minimized to zero by allocating weights inversely proportional to standard deviations:
  $$X_{SP} = \frac{\sigma_{SD}}{\sigma_{SP} + \sigma_{SD}} \approx 66.63\%, \quad X_{SD} = \frac{\sigma_{SP}}{\sigma_{SP} + \sigma_{SD}} \approx 33.37\%$$
  Due to the actual correlation being $\rho = -0.9989$ (not exactly $-1$), the resulting portfolio daily standard deviation is extremely small but non-zero ($0.000346$).
* **T-Bill Statistics**: The 13-week T-Bill annualized rate has a mean of $2.215\%$ and standard deviation of $1.869\%$.
* **Performance vs. T-Bills**: The zero-risk SPY/SDS portfolio has a lower annualized volatility and lower mean return than T-Bills, yet it yields a much higher Reward-to-Risk ratio (mean/std) because T-Bills suffer from higher volatility drag over time.

### 2. Beta, Covariance, & Minimum-Variance Allocations (Questions 5–10)
* **Gold Beta**: The monthly beta of Gold with respect to the S&P 500 is positive but less than $0.1$.
* **US Dollar (UUP) Beta**: The monthly beta of the US Dollar with respect to the S&P 500 is negative, sitting between $-0.25$ and $-0.20$.
* **S&P 500 & Gold Portfolio**: The risk-minimizing allocation to Gold is approximately $45.1\%$, which yields an annualized portfolio volatility of roughly $12.0\%$.
* **S&P 500 & US Dollar Portfolio**: The risk-minimizing allocation to the US Dollar is approximately $72\%$, leaving $28\%$ allocated to US Equity. This combination yields a monthly standard deviation of $\approx 1.25\%$, which is significantly lower than the S&P 500 & Gold portfolio.

### 3. Rolling Correlations & Market Regimes (Questions 11–14)
* **Rolling Correlations**: Analysis of 52-week rolling correlation between S&P 500 and the US Dollar shows significant regime shifts, dropping to deeply negative regions (e.g., after the 2008 financial crisis and around 2017/2018).
* **Three-State Market Regimes**: Partitioning weekly S&P 500 returns into High, Medium, and Low correlation regimes (using the 25th and 75th percentiles of rolling correlations) reveals that median returns are highest during the low correlation regime.
* **Hedging S&P 500 with US Dollar (UUP)**: Hedging a $2,000,000 position in SPY using UUP requires a long UUP position of approximately $\$3.5\text{M}$ to $\$4\text{M}$. However, the $R^2$ of this hedge is only around $13\%$, meaning it eliminates only a small fraction of the S&P 500 variance.

### 4. Global Minimum-Variance Portfolio (Questions 15–17)
* **Asset Allocation**: Allowing short sales across S&P 500, Gold, Commodities, and US Dollar, the Global Minimum Variance Portfolio (GMVP) places the highest weight on the **US Dollar**.
* **Reward-to-Risk**: The GMVP yields the highest Reward-to-Risk ratio among all individual assets.
* **Growth of $\$1$**: Over the historical dataset, the GMVP underperforms the S&P 500 in absolute dollar growth terms due to its conservative risk profile, despite S&P 500's volatility drag.

---

## 🛠️ Installation & Setup

To run the notebook and reproduce the results, set up a virtual environment and install the required dependencies:

1. **Activate the Virtual Environment**:
   * On Windows:
     ```powershell
     .\.venv\Scripts\activate
     ```
   * On macOS/Linux:
     ```bash
     source .venv/bin/activate
     ```

2. **Run Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```
   Open [`solutions.ipynb`](file:///c:/Users/User/Desktop/Projects/daily-returns/solutions.ipynb) to inspect or execute the code cells.

---

## 🗂️ File Directory structure

```
daily-returns/
├── .venv/                      # Python virtual environment
├── Question 1.docx             # Document detailing questions and answers
├── solutions.ipynb             # Jupyter Notebook with calculations & output
├── daily_prices_SPY_SDS_SSO.csv# Daily pricing data
├── daily_yield_irx.csv         # Daily T-bill yields
├── sp_gold_commodities_usd.csv # Monthly asset data
├── sp_bonds_gold_commodities_US$_weekly_px.csv # Weekly asset data
└── README.md                   # Project documentation
```
