# Financial Data Science Project — Plan & Context

## Who I am (starting point — be honest with me about this)

- High school junior at NCSSM (North Carolina School of Science and Mathematics)
- **Python experience:** basic only — syntax, logic, Boolean logic, arithmetic operators from coursework. No real project-building experience.
- **Data science / pandas / AI-ML experience:** effectively zero. This is the actual skill gap I'm trying to close.
- **Financial background:** real and substantive — VP of Finance for school DECA chapter (grants/sponsorships), currently running the DECA Stock Market Game (managing a live $100K virtual portfolio, competition started Sept 2026), prior equity research experience.
- **Goal:** build genuine, understood data science skill in the context of financial data, not just produce a finished-looking project I can't explain.

## Mentor context

I'm being informally mentored by **Justin Rowland**, a Data Analytics Instructor at Wake Tech Community College, with prior industry experience at SAS, Epic Games, and MaxPoint. This is not a formal internship — it's an informal mentorship that started from a cold email, a 30-minute intro call, and some async emails since.

### What Rowland has actually told me, directly
This is the real, complete list. I want to be careful not to inflate it into more than it is:
1. What data science is, broadly, as a field.
2. Where it gets applied, including in finance.
3. Start with something simple and develop/iterate from there — concretely, an entry-level regression (`y = mx + b`): pick one variable, try to predict another from it, and see how well it works.

That's it. He hasn't (yet) taught me train/test splitting, `statsmodels`, standard errors/hypothesis testing, or any of the heavier statistics that show up later in this project (see `v3_advanced_extension.ipynb`) — those are my own extension, built with AI assistance and disclosed as such.

### My own plan and assumptions, built on top of that
Everything below this point is *my* interpretation and *my* plan for running this project — not additional instructions from Rowland. I'm writing it down so I don't lose track of my own reasoning, but it should read as "what I decided," not "what he said":
- My own choice: approach this in a statistics-heavy way — understand the stats underlying any model, not just the code — since that's the natural direction once the "simple" version starts raising questions.
- My own assumption: building subject-matter expertise in finance alongside the technical skill is worth doing, since finance is a domain I already know something about (DECA, equity research). Rowland didn't tell me to do this; it's my own reasoning about how to use the time.
- My own environment choice: using the Anaconda distribution with Jupyter Notebook, since it's a common, well-supported setup for this kind of work — not something he required.
- My own standard, not a rule he handed me: I want to be able to explain any AI-assisted code before I run it. I've disclosed to him (and to my school) that I'm using AI assistance, and neither has objected, but "understand it before you run it" is discipline I'm holding myself to, not a line from him.
- My own read on structure: rather than working one of his existing projects, I'm picking my own topic, building it out, and bringing it to him for feedback — that's how an informal, self-directed mentorship like this seems like it should work, not something he laid out as a rule.
- My own read on scope: there's a huge amount of free financial data and APIs out there, so the actual work on my end is finding a specific, well-scoped "crux" question rather than trying to explore everything at once.
- My own assumption on cadence: I'm aiming to check in with him roughly every couple of weeks with real, even rough, progress — that felt like a reasonable rhythm for this kind of relationship, but it isn't a schedule we've formally locked in.

## Working philosophy for this project

**Updated 2026-09-09:** switched from build-with-me-incrementally to build-it-end-to-end.
Reasoning (my own words): "this is your project, do absolutely everything and just
explain at the end." My own standard for this was never "review every line as it's
written" — it's that I need to be able to explain the code, not just run it. Those are
different constraints, so the explanation step below is still mandatory and still has
to be real, just delivered after the build instead of gating each cell.

1. **Build the full project end-to-end without stopping for incremental sign-off.**
   Do not pause after each cell to check in — get to a complete, working version.
2. **Favor fewer, well-understood lines over comprehensive, opaque ones.** Simple,
   explainable code over compact/clever code, so the after-the-fact walkthrough is
   actually straightforward to follow.
3. **After the build is done, walk through the whole thing** — every cell, what it
   does, why it's there, and the statistics behind it (regression, R², correlation,
   volatility, etc.) — thoroughly enough that I could explain it to Rowland unaided,
   not just a high-level summary.
4. **This is a learning project, not a production system.** Prioritize clarity and my
   eventual comprehension over elegance, performance, or scale.
5. I am using AI assistance throughout — something I've disclosed to my mentor and to
   my school, and neither has objected — the constraint I'm holding myself to is
   comprehension, not tool usage.

## The actual project scope

**Type:** Entry-level predictive modeling project using real financial data (per Rowland's suggestion).

**Starting concept:** Basic regression — using one or more variables (e.g., price history, trading volume, a moving average) to predict a financial outcome (e.g., next-day price, direction of price movement). Start as simple as a single-variable linear regression before adding complexity.

**Data source:** To be determined — likely a free financial API (e.g., yfinance, Alpha Vantage) rather than a static dataset, since I want to work with real, live-ish financial data.

**Possible topic directions considered, and the crux chosen (2026-09-09):**
- ~~Predicting next-day stock price from today's price/volume~~ — rejected: regressing
  price levels on price levels looks deceptively good (high R²) purely because prices
  are a near-random walk, not because the model learned anything real.
- ~~Predicting price direction (up/down)~~ — rejected as the starting point: it's
  classification, not the regression Rowland suggested, and direction-from-price-alone
  tends to hover near a coin flip.
- ~~Tied to my DECA Stock Market Game holdings~~ — explicitly rejected by me: "it
  doesn't have to be DECA stock related, in fact I don't want it to be, it was just my
  experience." I let the topic stay open rather than picking something tied to my portfolio.
- **Chosen crux: estimate a stock's market beta via simple linear regression of its
  daily returns against a market benchmark's (S&P 500 / SPY) daily returns** —
  `stock_return = β · market_return + α`. Uses returns, not price levels, which avoids
  the random-walk trap above while still being a single-variable `y = mx + b` model, a
  real finance concept (systematic risk / CAPM), and a clean predicted-vs-actual plot.

**Scope philosophy:** Start as small and complete as possible. A finished, simple, understood project beats an ambitious, half-built one. Scale up complexity only after the first version is solid and I can explain every part of it.

## Environment setup needed

- Install Anaconda distribution
- Confirm Jupyter Notebook launches and runs a basic cell
- Standard libraries expected: pandas, numpy, matplotlib, scikit-learn (for basic regression), and a financial data API library (e.g., yfinance)

## Timeline

- **Weeks 1–4:** Environment setup, work through any labs/videos/materials Rowland sends plus stuff I find on my own, pick the specific project topic ("crux"), build the entry-level regression model with real understanding of each step.
- **Weeks 4–8:** Scale up the project (more features, better evaluation, cleaner visualization), incorporate feedback from Rowland's check-ins.
- **~Week 8:** Project reaches a genuinely presentable state. Plan to publish it (LinkedIn post + possibly GitHub).
- **Check-ins with Rowland:** roughly every couple of weeks (my own aim, not a fixed schedule we've agreed to), bringing real (even rough/incomplete) progress each time — not polished status updates.

## What "done" looks like for version 1

- A working Jupyter Notebook that:
  1. Pulls real financial data via an API
  2. Cleans/prepares the data
  3. Builds a simple regression model
  4. Evaluates how good the model actually is (not just that it runs)
  5. Produces at least one clear visualization (e.g., predicted vs. actual)
- I can explain every step out loud, unaided, without reading from notes.

## Longer-term goal (context, not immediate scope)

Once this project is solid, the plan is to:
1. Publish it on LinkedIn, honestly framed as an "Independent Researcher" project (self-directed, real methodology, mentorship credited to Justin Rowland) — not an inflated title.
2. Send honest follow-up notes to professors I previously cold-emailed (at NC State, Duke, UNC — several in finance/fintech/ML-adjacent research), referencing this finished project as proof of follow-through, to try to find a small way to contribute to their research.
3. If a professor says yes to something concrete and ongoing, that becomes the basis for a legitimate "Student Researcher" or "Research Assistant" title — only once actually true, with a named supervisor and real assigned tasks (not before).

This document should be treated as the current source of truth for the project's goals, constraints, and working style. If anything here becomes outdated (e.g., Rowland's materials change the plan, or the topic changes), update this file rather than working from stale assumptions.

---

## Running log (lab notes)

Honest record of what was tried and what it showed — material for the check-ins with
Rowland. Keeping it rough and honest here is my own choice, not something he demanded.

### 2026-09-09 — v1 built end-to-end (`stock_beta_regression.ipynb`)

**What was built:** AAPL daily returns regressed on SPY daily returns, 2 years of
daily data via yfinance, `LinearRegression` from scikit-learn, time-ordered 80/20
train/test split, evaluated with R² and correlation, two plots saved to
`beta_regression_plot.png`.

**Results as run (data through 2026-09-08):**

| | train (2024-09-11 → 2026-04-15) | test (2026-04-16 → 2026-09-08) |
|---|---|---|
| beta | 1.176 | — (model not refit) |
| R² | 0.501 | **−0.100** |
| correlation | 0.708 | 0.158 |
| AAPL daily return std | 0.0182 | 0.0182 |
| SPY daily return std | 0.0110 | 0.0079 |

Full-period beta (no split, closer to how beta is normally published): **1.085**,
R² 0.385.

**Decisions made and why:**
- *Returns, not price levels.* Regressing price on price gives a near-perfect R²
  purely because prices barely move day to day (random walk). Returns remove that
  artifact. This is why beta is universally defined on returns.
- *`shuffle=False` on the train/test split.* A random shuffle would leak future days
  into the training set. Splitting in time order means the test period is genuinely
  "data the model hasn't seen," which is the only honest test for time series.
- *Kept a separate full-period fit.* The split answers "is this relationship stable?";
  the full-period fit answers "what is AAPL's beta?" Those are different questions and
  needed different fits.

**The actual finding (and it was not the one expected):** the model failed
out-of-sample. Test R² came out **negative**, meaning the fitted line predicted the
test period *worse than just guessing the average daily return*. Verified rather than
assumed: predicting the training mean on the test set scores R² ≈ −0.01, so the
model at −0.10 is genuinely below that baseline; and test residual std (0.0194) is
larger than AAPL's own test std (0.0183) — the "explanation" adds variance.

**Why it happened:** refitting beta on the test period alone drops it from 1.18 to
**0.32**, with an in-sample R² of just 0.018. In that stretch AAPL essentially
decoupled from the market. The largest misses are all days where SPY barely moved and
AAPL moved hard (e.g. 2026-07-31: SPY +0.7%, AAPL −7.4%) — stock-specific news, which
a market-return-only model has no way to see. Note also SPY's volatility fell (0.0110 →
0.0079) while AAPL's held flat (0.0182) — the market got calm, AAPL didn't.

**Takeaway:** beta is a historical tendency, not a constant. This is the concrete
reason practitioners quote *rolling* beta rather than one fixed number.

**Open questions for Rowland:**
1. Is a negative out-of-sample R² the right thing to report as the headline, or is the
   more standard framing to report full-period beta with a confidence interval?
2. Should beta be estimated on a rolling window instead of one fixed split?
3. `LinearRegression` gives no standard errors or p-values on the slope. Is
   `statsmodels.OLS` the expected tool once inference matters, given my own
   statistics-heavy approach to this?

**Known gaps in v1:** no standard error / confidence interval on beta; no residual
diagnostics (normality, heteroskedasticity, autocorrelation); single stock, single
benchmark; no risk-free rate, so alpha here is raw excess return, not CAPM alpha.

### 2026-09-13 — v2 built (`beta_regime_analysis.ipynb`), 54 cells, 6 figures

v1 ended with an unexplained result: the model failed out-of-sample, test R² negative,
beta refit on the test window = 0.32 vs 1.18 on training. v2 exists to answer whether
that was noise or real. **It was real, and it turned out not to be about Apple.**

**Scope change from v1:** 2y → 5y, one stock → 11 stocks + 2 benchmarks (SPY
cap-weighted, RSP equal-weighted), raw returns → excess returns over the 13-week
T-bill (`^IRX`), and `sklearn.LinearRegression` → `statsmodels.OLS` so estimates come
with standard errors. Carrying 11 stocks instead of 1 is what made the real finding
visible at all.

**The investigation, in the order it actually happened:**

1. **Baseline (5y, excess returns).** beta 1.172, SE 0.032, 95% CI [1.109, 1.235],
   R² 0.516. Tested H0: β = 1 (not β = 0, which nobody asks) → t = 5.35, rejected.
   Alpha p = 0.56 — **not** distinguishable from zero.
2. **Diagnostics.** Normality rejected hard (kurtosis 7.63 vs 3). Breusch-Pagan clean
   (p = 0.33). But Ljung-Box on *squared* residuals p ≈ 0 → volatility clustering, which
   breaks the independence assumption and makes plain SEs too small. Fixed with HAC /
   Newey-West: SE inflates 47%, CI widens to [1.079, 1.264]. Conclusion survived.
3. **Chow test at the pre-specified 80/20 split:** F = 15.14, p = 3.2e-07. Stability
   rejected. sup-F scan over 877 candidate dates peaks at **2025-10-28**, F = 18.23,
   which clears the Andrews sup-Wald 5% bar (~12.4) that applies once you search.
4. **Hypothesis "something happened at Apple" — FALSIFIED.** 10 of 11 stocks' betas
   fell, mean change −0.399. Five defensives went negative. Mean R² fell 0.285 → 0.126.
5. **Hypothesis "it's S&P index concentration / the AI mega-caps" — FALSIFIED.** Mean
   beta change vs cap-weighted SPY −0.399, vs equal-weighted RSP −0.392. Identical.
   This is why RSP was downloaded; it was the control that killed my own explanation.
6. **Actual mechanism: correlation collapse.** Using β = corr × (σ_stock/σ_market):
   mean corr 0.497 → 0.165, mean vol ratio 1.638 → 2.101. Counterfactuals: correlation
   alone would have taken beta 0.815 → 0.270; the vol ratio alone would have pushed it
   *up* to 1.045. Correlation did all the work and then some. Avg pairwise correlation
   among the 11 stocks: 0.254 → 0.058. Index vol fell 18% → 13% while single-stock vol
   barely moved (29.4% → 27.4%) — an index is a portfolio, so when its components stop
   agreeing it diversifies itself calm.
7. **Robustness.** Dropping the top 5% of market days moves mean beta ≤0.013. Four
   arbitrary calendar splits all reproduce it. **But** current 60-day correlation sits at
   only the 22nd percentile of its own 5y history — low, cyclical, *not* unprecedented.
   That check is the one that stopped me overclaiming a "new regime."
8. **Which beta to quote.** Six defensible estimates spanning 0.685–1.171 depending only
   on window and frequency (5y monthly = Yahoo's method = 1.069; 2y weekly = Bloomberg's
   = 1.070). Five overlap; the 1y daily outlier is measuring the post-break regime.
9. **Blume shrinkage tested rather than quoted.** 0.67β + 0.33 made next-year prediction
   *worse* on this sample (RMSE 0.337 vs 0.300); best-fitting weight ≈ 0.94, pooled fit
   `next = 0.932·past + 0.035`. Not a refutation of Blume — 11 hand-picked large-caps is
   a convenience sample and Blume's constant came from a broad universe. The honest
   lesson is that the shrinkage constant is a property of the universe and is checkable.

**What broke along the way (worth remembering):**
- `.venv/bin/pip` is dead: the venv was created while this folder was named
  "untitled folder" and the shebang still points there. **Use `.venv/bin/python -m pip`**
  — it works. (Or rebuild the venv.)
- `statsmodels` wasn't installed; it is now (0.15.0).
- pandas 3.0 removed `DataFrame.last("730D")` — use boolean index slicing on the date.
- `statsmodels.stats.stattools.jarque_bera` returns **raw** kurtosis (normal = 3), not
  excess kurtosis (normal = 0). I mislabelled it in a first draft and had to fix it.

**Honest caveats now written into §10 of the notebook:** every regression is
contemporaneous (same-day market return explains same-day stock return), so nothing here
forecasts anything; AAPL is itself ~7% of SPY so part of the co-movement is arithmetic;
the break *date* is poorly identified even though the break's *existence* is not (the
sup-F curve is a broad plateau, not a spike); fat tails are diagnosed but unmodelled.

**For Rowland:**
1. Is sup-Wald with the Andrews critical value the right tool here, or would he expect
   CUSUM / a Bai-Perron multiple-break test?
2. The rolling-beta chart shows beta wandering continuously. Is the two-regime framing
   defensible at all, or should this just be a time-varying-beta (Kalman/DCC) project?
3. Is testing Blume on 11 stocks worth reporting, or too small a sample to mention?

**Next:** add Fama-French factors (§4 says ~half of AAPL's variance is unexplained by
the market — some of it is probably size/value/momentum, not true idiosyncrasy); model
the volatility clustering with GARCH instead of only correcting for it; widen to a few
hundred stocks before saying anything more about shrinkage.
