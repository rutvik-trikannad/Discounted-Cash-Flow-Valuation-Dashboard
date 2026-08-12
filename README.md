# DCF Valuation Dashboard

An interactive discounted cash flow model built in Python. Enter any stock ticker and it pulls live financials via yfinance, auto-calculates WACC through CAPM, and lets every assumption (growth rate, EBIT margin, tax rate, terminal method) be adjusted manually or left on auto.

Generates Bull/Base/Bear scenario valuations, a WACC-vs-terminal-growth sensitivity heatmap, and a 20,000-iteration Monte Carlo simulation of intrinsic value.

Built as a working prototype: functional end-to-end for any US-listed ticker, with room for refinement.

## Files
- `DCF_Valuation_Dashboard.ipynb` — the notebook
- `requirements.txt` — Python dependencies

## Requirements

Run in Jupyter or Google Colab with an active internet connection (for live data via yfinance). Install dependencies with: `pip install -r requirements.txt`

- **yfinance** — pulls live stock prices and financial statements
- **ipywidgets** — powers the interactive sliders and buttons
- **pandas** / **numpy** — data handling and calculations
- **matplotlib** / **seaborn** — charts and the Monte Carlo distribution plot