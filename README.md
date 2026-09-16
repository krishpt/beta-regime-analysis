# Is beta a number, or a regime?

I built this project to figure out how much a stock actually moves with the market, and whether that number (called beta) even stays the same over time. It's a self directed data science project I'm doing with informal mentorship from Justin Rowland, who teaches data analytics at Wake Tech Community College and worked at SAS, Epic Games, and MaxPoint before that.

I'm a total beginner at this. Basic Python from school, no real pandas or machine learning background going in. **The main notebook to read is `notebooks/beta_explained_simply.ipynb`.** It only uses linear regression, correlation, and plotting, and it's the one I can actually explain start to finish. I also built a second, much more advanced version with real statistics (`notebooks/v3_advanced_extension.ipynb`), which I'm calling out honestly below.

## What I was actually trying to answer

Beta is just the slope of a line: `stock_return = beta * market_return + alpha`. If beta is 1.2, the stock tends to move 20% more than the market on a given day, same direction. It's a basic linear regression, which is why my mentor suggested it as a starting point.

My first version (`notebooks/v1_stock_beta_regression.ipynb`) used two years of Apple data and split it into a training period and a test period, like you're supposed to. The training R squared looked fine. Then I ran it on the test period and got a NEGATIVE R squared, which means the model did worse than just guessing the average return every day. That's not supposed to happen, and I didn't expect it.

I could've just called that a fluke and moved on. Instead I wanted to actually know whether it was noise or a real change.

## What I found (the beginner version, `beta_explained_simply.ipynb`)

- Beta isn't fixed. I recomputed it every 60 trading days over 5 years and it moves around constantly, dropping sharply near the end of the data.
- I checked 10 other well known stocks besides Apple, and 10 of the 11 had their beta fall over that same stretch. Not an Apple thing.
- My next guess was that the S&P 500 is weighted toward a few huge companies and that's warping things. I tested that against an equal weighted version of the same 500 stocks (RSP) and got almost the exact same drop, so that guess didn't hold up either.
- What actually happened: the 11 stocks stopped moving together as much. Their correlation with each other dropped from about 0.25 to about 0.06. Beta is partly built out of that correlation, so when it fell, beta fell with it, for almost every stock at once.

That's the real finding, and it's the same finding whether you look at the beginner notebook or the advanced one below. I just didn't need graduate level statistics to see it.

## The advanced version, and why it's separate

`notebooks/v3_advanced_extension.ipynb` runs the same question through actual statistical inference: standard errors, hypothesis tests, a Chow test for the exact break point, residual diagnostics, and a test of a shrinkage rule that Bloomberg uses for beta. I built it because I wanted to see if the beginner finding held up under real statistical scrutiny, and it does. But I'm not going to pretend I fully understand every method in there yet. I used AI assistance to build it, the same way I used AI assistance throughout this whole project, with my mentor's and my school's approval. I'm keeping it in the repo because the extra rigor is real and I want to eventually grow into actually understanding it, not because I'm claiming I already do.

## Files

- `notebooks/beta_explained_simply.ipynb` - the version I can fully explain, start to finish
- `notebooks/v1_stock_beta_regression.ipynb` - my first attempt, single stock, where the negative test R squared first showed up
- `notebooks/v3_advanced_extension.ipynb` - the statistically rigorous version, built with heavier AI assistance, still learning this part
- `figures/` - charts from all three notebooks
- `PROJECT_NOTES.md` - my running lab notes, including what broke along the way and what I still want to ask my mentor
- `requirements.txt` - exact package versions

## Running it

```
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/beta_explained_simply.ipynb
```

The data comes straight from Yahoo Finance through `yfinance`, so if you run this again later the exact numbers will shift a little, since new trading days keep getting added. The numbers and charts in this repo are from the run I committed.

## Why this exists

The standard I'm holding myself to for this project isn't "review every line before you run it." It's that I need to be able to explain what the code is doing and why, not just get it to run — that's a bar I set for myself, not a rule my mentor handed down. `PROJECT_NOTES.md` is where I kept track of that honestly as I went, including the parts that didn't work the first time.

## License

MIT, see [LICENSE](LICENSE).
