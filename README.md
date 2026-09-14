# Is Beta a Number, or a Regime?

### Estimating market beta via linear regression — and finding out it doesn't hold still

An independent data science project applying regression to real financial data:
estimating a stock's **market beta** — the slope of `stock_return = β · market_return + α` —
and testing, rather than assuming, whether that slope is actually stable over time.

**Author:** Krish P. — high school student, self-directed project
**Mentor:** Justin Rowland, Data Analytics Instructor, Wake Tech Community College
(prior industry experience at SAS, Epic Games, MaxPoint)

---

## The question

Beta is the single number finance uses to describe how much a stock moves when the
market moves. It comes straight out of a simple linear regression — literally `y = mx + b`.

**Version 1** (`notebooks/v1_stock_beta_regression.ipynb`) estimated Apple's beta on two
years of daily data, split the data into train/test periods, and got a result that wasn't
supposed to happen: the model **failed out-of-sample**. Fit on the first 80% of days,
tested on the last 20%, the test R² came out *negative* — the fitted line predicted the
recent period worse than just guessing the average return.

That's either noise, or a real change in how the stock relates to the market. A plain
`sklearn.LinearRegression` can't tell you which, because it returns a slope and nothing
else — no standard error, no confidence interval, no way to test a hypothesis.

**Version 2** (`notebooks/v2_beta_regime_analysis.ipynb`) exists to answer that question
properly, using `statsmodels` for real statistical inference. The short version: **it was
real, and it wasn't about Apple.**

## What v2 actually found

1. Apple's 5-year beta is **1.17** (95% HAC CI: **[1.08, 1.26]**) — statistically distinct
   from 1. Alpha is **not** distinguishable from zero.
2. A **Chow test** rejects the hypothesis that beta stayed constant (p < 0.0001). A scan
   for the most likely break date lands on **late October 2025**, beta falling from ~1.23
   to ~0.60.
3. Widening the analysis to 11 stocks shows the break is **not an Apple story** — 10 of 11
   stocks' betas fell over the same window.
4. It's also **not S&P index concentration** — the effect is identical against an
   equal-weighted benchmark (RSP) as against the cap-weighted S&P 500 (SPY), which rules out
   "a few mega-caps are distorting the index."
5. The actual mechanism: **average pairwise correlation among the 11 stocks collapsed**
   from ~0.25 to ~0.06. Decomposing `beta = correlation × volatility ratio` shows the
   correlation collapse did all the work, while the volatility ratio moved the other way.
6. That correlation level is low but **not unprecedented** — it sits around the 22nd
   percentile of its own 5-year range, which keeps the finding from being overclaimed as a
   "new regime."
7. A textbook rule (Blume 1971 shrinkage, `0.67·β + 0.33`, still used by Bloomberg) is
   tested rather than quoted, and it makes prediction *worse* on this sample — with the
   reasons for that discrepancy discussed rather than left hanging.

Full reasoning, every statistical test, every robustness check, and the honest limitations
are walked through in the notebook itself — this README is a summary, not a substitute.

## Repository structure

```
notebooks/
  v1_stock_beta_regression.ipynb    single-stock regression, train/test split (the starting point)
  v2_beta_regime_analysis.ipynb     11-stock regime analysis with full statistical inference
figures/
  v1_beta_regression_plot.png       v1's predicted-vs-actual plot
  fig3_diagnostics.png              residual diagnostics (normality, autocorrelation, volatility clustering)
  fig4_risk_decomposition.png       systematic vs. idiosyncratic risk, all 11 stocks
  fig5_break_scan.png               structural break test across every candidate date
  fig6_rolling_beta.png             beta and cross-stock correlation over time
  fig7_cross_section.png            before/after beta, all 11 stocks (the "not an Apple story" chart)
  fig8_which_beta.png               six defensible beta estimates by window/frequency
PROJECT_NOTES.md                    running lab notes — what was tried, what broke, open questions
requirements.txt
```

## Running it

```bash
python -m venv .venv && source .venv/bin/activate   # or: conda create -n beta python=3.11
pip install -r requirements.txt
jupyter notebook notebooks/v2_beta_regime_analysis.ipynb
```

Data is pulled live from Yahoo Finance via `yfinance`, so re-running the notebook later
will shift the exact numbers slightly as new trading days arrive — the commentary reflects
the run committed here.

## Methods used

Linear regression (OLS) · robust (HAC/Newey–West) standard errors · hypothesis testing on
regression coefficients · residual diagnostics (Jarque–Bera, Breusch–Pagan, Ljung–Box) ·
Chow structural break test · Quandt–Andrews sup-Wald break-date search · rolling-window
estimation · variance decomposition · out-of-sample validation.

## Context

This project was built under the guidance of Justin Rowland as an entry point into
statistics-heavy financial data science — the goal being real, explainable understanding
of the methodology rather than a polished result produced without comprehension. `PROJECT_NOTES.md`
keeps an honest running log, including what broke and open questions still being discussed
with him.

## License

MIT — see [LICENSE](LICENSE).
