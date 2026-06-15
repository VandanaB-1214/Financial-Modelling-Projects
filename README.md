#  Quantitative Financial Analysis in R
### A Collection of Financial Modelling Studies Using Real-World Market Data

> **Purdue University | MS Business Analytics & Information Management**
> Author: Vandana Brahmasa

---

##  Overview

This repository contains a series of quantitative finance analyses conducted using R, exploring foundational questions in financial economics: How do we estimate expected returns? Can past returns predict future ones? How does randomness and probability explain casino economics? Did stocks beat inflation in the stagflation era of the 1970s?

Each analysis draws on **real historical market data** — including Robert Shiller's dataset spanning 150+ years of U.S. stock market history and Federal Reserve economic data — to answer these questions empirically.

---

##  Repository Contents

| File | Analysis | Key Methods |
|---|---|---|
| `Lab10_Expected_Returns.Rmd` | Estimating expected U.S. stock returns since 1871 | Mean returns, standard error, confidence intervals, subsample analysis |
| `Lab11_Return_Predictability.Rmd` | Can last month's return predict next month's? | Autocorrelation (ACF), time series regression, annual vs monthly analysis |
| `Lab13_Casino_Simulation.Rmd` | How casinos guarantee profit through probability | Monte Carlo simulation, expected value, law of large numbers |
| `Lab6_Inflation_vs_StockReturns.Rmd` | Did stocks beat inflation in the 1970s? | S&P 500 vs CPI comparison, index normalization, FRED data integration |

---

##  Analysis Summaries

---

### Lab 10 — Estimating Expected Stock Returns
**Data:** Robert Shiller's S&P Composite Index (1871–present)

The expected return on stocks is one of the most important — and most debated — numbers in finance. This analysis estimates it empirically using 150+ years of monthly U.S. stock market data, accounting for dividends in return calculations.

**Approach:**
- Loaded Shiller dataset (xts format) via `quantmod`
- Calculated monthly total returns: `(Price + Dividend/12) / lag(Price) - 1`
- Estimated expected return as the sample mean
- Computed standard error: `sd / sqrt(n)`
- Constructed 95% confidence interval using z-score of 1.96
- Repeated analysis on post-WWII subsample (1946–present) to examine the tradeoff between sample size and relevance

**Key Finding:** The confidence interval for expected returns is surprisingly wide, illustrating why even 150 years of data leaves meaningful uncertainty in this estimate — a key insight in financial economics. The post-WWII subsample yields a higher point estimate but with greater uncertainty due to the smaller sample.

**Tools:** `R`, `quantmod`, `xts`

---

### Lab 11 — Return Predictability
**Data:** Robert Shiller's S&P Composite Index — monthly (1871–present) and annual (1871–present)

The Efficient Market Hypothesis suggests past returns should not predict future returns. This analysis tests that directly using autocorrelation analysis and regression on both monthly and annual data.

**Approach:**
- **Part I (Monthly):** Calculated monthly S&P returns; used `acf()` to plot autocorrelation structure; regressed current month's return on prior month's return using `lm()`
- **Part II (Annual):** Loaded Shiller annual dataset; converted to `xts`; calculated annual returns using the dividend-timing-adjusted formula `rt = (P(t+1) + div(t)) / P(t) - 1`; repeated autocorrelation and regression analysis

**Key Finding:** Monthly returns show little to no autocorrelation — consistent with market efficiency at short horizons. Annual returns show stronger autocorrelation patterns, suggesting some degree of mean-reversion over longer time horizons — a well-documented phenomenon in financial economics.

**Tools:** `R`, `quantmod`, `xts`, `lm()`

---

### Lab 13 — How to Run a Casino: Monte Carlo Simulation
**Concept:** Probability, Expected Value, Law of Large Numbers

Why do casinos prefer slot machines (small, frequent bets) over high-stakes single bets? This simulation-based analysis answers that question by demonstrating how the Law of Large Numbers turns a small house edge into near-certain profit.

**Approach:**
Three scenarios — all with identical 2% house edge:

| Scenario | Stake | Rounds | Simulations |
|---|---|---|---|
| A | $10,000 | 1 | Analytical |
| B | $100 | 100 | 10,000 Monte Carlo iterations |
| C | $1 | 10,000 | 10,000 Monte Carlo iterations |

- Used `sample()` for coin toss simulation
- Ran 10,000 simulation iterations per scenario using `for` loops
- Calculated expected casino profit and probability of profit per scenario

**Key Finding:** With a single high-stakes bet, the casino has only a 50% chance of profit despite its edge. With 10,000 small bets at the same edge, the casino's probability of profit approaches near-certainty (~97%+). The house edge is the same — only the number of trials changes. This is the Law of Large Numbers in action, and it explains why casinos are designed the way they are.

**Tools:** `R`, `sample()`, Monte Carlo simulation

---

### Lab 6 — Did Stocks Beat Inflation in the 1970s?
**Data:** S&P 500 (Yahoo Finance via `quantmod`), CPI-U (Federal Reserve FRED database)

The 1970s were defined by stagflation — simultaneously high inflation and stagnant economic growth. This open-ended research analysis examines whether equity investments kept pace with or outpaced inflation during this period.

**Approach:**
- Retrieved S&P 500 price data (1970–1979) using `getSymbols()` from Yahoo Finance
- Retrieved seasonally adjusted CPI data (CPIAUCSL) from the **Federal Reserve FRED** database
- Converted both series to monthly frequency and aligned date indices
- Normalized both series to a base of 100 at January 1970 for direct comparison
- Merged and plotted both series on a single chart

**Key Finding:** Inflation (CPI) outpaced S&P 500 returns throughout the 1970s — stocks failed to beat inflation during this decade. This aligns with the historical record: the 1970s were one of the worst decades for real equity returns in U.S. history, driven by oil shocks, Federal Reserve policy constraints, and broad economic stagnation.

**Tools:** `R`, `quantmod`, `xts`, `FRED` API

---

##  Tools & Libraries

```r
library(quantmod)   # Financial data retrieval and xts manipulation
library(xts)        # Time series data structures
# Base R: lm(), acf(), sample(), mean(), sd(), plot()
```

**Data Sources:**
- Robert Shiller's Stock Market Data (1871–present): [econ.yale.edu/~shiller](http://www.econ.yale.edu/~shiller/data.htm)
- S&P 500 Price Data: Yahoo Finance via `quantmod::getSymbols()`
- Consumer Price Index (CPIAUCSL): Federal Reserve FRED database

---

##  How to Run

1. Clone this repository
2. Open any `.Rmd` file in RStudio
3. Install required packages if needed:
```r
install.packages(c("quantmod", "xts"))
```
4. Click **Knit** to render the full analysis as an HTML document, or run code chunks individually

> **Note:** Labs 10 and 11 load data from Purdue University's servers via URL. An internet connection is required to run those notebooks.

---

## Context

These analyses were completed as part of a **Financial Modelling** course in the MS Business Analytics & Information Management program at **Purdue University, Daniels School of Business** (Spring 2025).

---

## Author

**Vandana Brahmasa**
[LinkedIn](https://www.linkedin.com/in/vandana-brahmasa) | [vandanabrahmasa92@gmail.com](mailto:vandanabrahmasa92@gmail.com)
