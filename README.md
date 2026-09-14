# Is beta a number, or a regime?

I built this project to figure out how much a stock actually moves with the market, and whether that number (called beta) even stays the same over time. It's a self directed data science project I'm doing with informal mentorship from Justin Rowland, who teaches data analytics at Wake Tech Community College and worked at SAS, Epic Games, and MaxPoint before that.

## What I was actually trying to answer

Beta is just the slope of a line: `stock_return = beta * market_return + alpha`. If beta is 1.2, the stock tends to move 20% more than the market on a given day, same direction. It's a basic linear regression, which is why my mentor suggested it as a starting point.

My first version (`notebooks/v1_stock_beta_regression.ipynb`) used two years of Apple data and split it into a training period and a test period, like you're supposed to. The training R squared looked fine. Then I ran it on the test period and got a NEGATIVE R squared, which means the model did worse than just guessing the average return every day. That's not supposed to happen, and I didn't expect it.

I could've just called that a fluke and moved on. Instead I wanted to actually know whether it was noise or a real change, and `sklearn` couldn't tell me that, since it only gives you a slope, not a standard error or a confidence interval.

## What I found in version 2

Version 2 (`notebooks/v2_beta_regime_analysis.ipynb`) switches to `statsmodels`, widens the data to 5 years, and adds 10 more stocks plus a second market benchmark. Here's what came out of it:

- Apple's beta over 5 years is 1.17, with a 95% confidence interval of [1.08, 1.26], so it's genuinely different from 1, not just noise. Alpha isn't different from zero though, meaning Apple didn't reliably beat what its market exposure alone would predict.
- A Chow test says beta was NOT stable across the 5 years (p < 0.0001). Scanning every possible break date points to late October 2025, where beta drops from about 1.23 to about 0.60.
- I first assumed this was an Apple thing. It wasn't. 10 out of 11 stocks I tested had their beta fall over the same stretch.
- I then thought maybe it was just that the S&P 500 is weighted toward a handful of huge companies. So I tested against an equal weighted version of the index too (RSP instead of SPY) and got almost the exact same drop, which ruled that out.
- What actually happened: the 11 stocks stopped moving together. Average correlation between them fell from about 0.25 to about 0.06. Beta is correlation times a volatility ratio, and the correlation drop did basically all the work, even though the volatility ratio moved the other way.
- That correlation level isn't some historic low, though, it's sitting around the 22nd percentile of its own 5 year range, so I'm not calling this an unprecedented new regime, just a low point in a cycle.
- I also tested the Blume shrinkage rule that Bloomberg still uses for adjusted beta (0.67 times beta plus 0.33) rather than just trusting it, and it actually made predictions worse on my data, not better.

Every test, every chart, and the full walkthrough of what each statistic actually means is in the notebook itself. This README is the summary, not the whole thing.

## Files

- `notebooks/v1_stock_beta_regression.ipynb` - the original single stock regression that first showed the negative test R squared
- `notebooks/v2_beta_regime_analysis.ipynb` - the full 11 stock regime analysis with real statistical inference
- `figures/` - every chart from both notebooks, already rendered as PNGs
- `PROJECT_NOTES.md` - my running lab notes, including what broke along the way and what I still want to ask my mentor
- `requirements.txt` - exact package versions

## Running it

```
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/v2_beta_regime_analysis.ipynb
```

The data comes straight from Yahoo Finance through `yfinance`, so if you run this again later the exact numbers will shift a little, since new trading days keep getting added. The numbers and charts in this repo are from the run I committed.

## Methods

OLS regression, HAC (Newey-West) standard errors, hypothesis tests on the regression coefficients, residual diagnostics (Jarque-Bera, Breusch-Pagan, Ljung-Box), a Chow structural break test, a Quandt-Andrews sup-Wald search for the break date, rolling window estimation, variance decomposition, and out of sample validation.

## Why this exists

My mentor's actual rule for this project was never "review every line before you run it." It was that I need to be able to explain what the code is doing and why, not just get it to run. `PROJECT_NOTES.md` is where I kept track of that honestly as I went, including the parts that didn't work the first time.

## License

MIT, see [LICENSE](LICENSE).
