# Discounted Cash Flow (DCF) Valuation Dashboard

An interactive DCF model in Python. Type in a stock ticker and the notebook pulls the company's financials from Yahoo Finance, builds a WACC with CAPM, values the business, and compares the result with the current share price. Every assumption can be left on auto or set by hand with sliders, so the model can be stress-tested without touching the code.

It is a working prototype that runs end to end for any U.S.-listed ticker. The notebook starts on MSFT.

## What it produces

1. **Intrinsic value per share** against the current price, with the upside or downside.
2. **Bear, Neutral, and Bull scenarios.** Bear cuts revenue growth and EBIT margin by 2 points each and adds 1 point to WACC. Bull does the reverse.
3. **A WACC and terminal growth heatmap.** Intrinsic value across 7 WACC values (2 points either side of the base) and 5 terminal growth values (1 point either side).
4. **A sensitivity table.** The dollar and percentage change in value from a 1 point increase in revenue growth, EBIT margin, or WACC, one at a time.
5. **A Monte Carlo simulation.** 20,000 runs that draw revenue growth (standard deviation of 2 points) and WACC (standard deviation of 1 point) around the base case, plotted as a distribution of intrinsic values against the base case and the market price.
6. **A written valuation summary** with the key assumptions, generated for whichever ticker is entered.

## How it works

- **Inputs on auto.** The risk-free rate comes from the live 10-year Treasury yield. Beta comes from Yahoo Finance and falls back to 1.0 if missing. The market risk premium is 6%. The tax rate is the effective rate from the income statement, with a 21% fallback. Cost of debt is interest expense over average debt, with a 5% fallback.
- **WACC.** CAPM cost of equity (risk-free rate plus beta times the market risk premium) and after-tax cost of debt, weighted by market cap and total debt.
- **Forecast.** Either a single-stage 5-year model, or a 10-year multi-stage model where growth starts high and fades in a straight line down to the terminal rate.
- **Terminal value.** Perpetuity growth, or an exit multiple on EBIT (12x by default). The model blocks any case where WACC is not above terminal growth.
- **Equity value.** Enterprise value minus net debt, divided by shares outstanding.

## Limits

- **Simplified free cash flow.** Forecast FCF is EBIT after tax. It does not subtract capex or changes in working capital, and it does not add back depreciation, so it works best for businesses with modest reinvestment needs.
- **Data quality.** Yahoo Finance fields are sometimes missing or inconsistent across companies. The notebook has fallbacks, but results for unusual companies should be checked by hand.
- **Random results.** The Monte Carlo simulation has no fixed seed, so its mean changes slightly each run.
- **Not advice.** This is a student project and not investment advice.

## Files

- `DCF_Valuation_Dashboard.ipynb`: the notebook
- `requirements.txt`: Python dependencies

## Running it

Open the notebook in Jupyter or Google Colab with an internet connection, since the data comes live from Yahoo Finance. Install the dependencies with `pip install -r requirements.txt`, run the cells in order, and enter a ticker in Step 1. The notebook uses ipywidgets for the sliders and buttons.
