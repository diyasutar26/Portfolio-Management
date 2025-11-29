# Portfolio Management with Python

This project demonstrates a complete workflow for downloading financial market data, cleaning multi-index structures returned by `yfinance`, and preparing a consolidated dataset of closing prices for multiple large-cap stocks and the S&P 500 index. The objective is to build a solid foundation for portfolio analytics, risk modeling, and factor-based strategies.

---

## 🚀 Project Overview

This repository contains:

- **Automated data extraction** using `yfinance`
- **Handling MultiIndex DataFrames** (a common headache in financial data work)
- **Column flattening utilities**
- **Consolidation of closing prices** across multiple assets
- **A clean, analysis‑ready dataset** suitable for portfolio analytics, regression models, risk attribution, and time‑series modeling.

The project focuses on large‑cap US equities:

- **GOOG (Alphabet)**  
- **AAPL (Apple)**  
- **META (Meta Platforms)**  
- **AMZN (Amazon)**  
- **MSFT (Microsoft)**  
- **^GSPC (S&P 500 Index)**  

Data is downloaded from **2012‑05‑18 to 2023‑01‑01**.

---

## 📁 Files Included

- `Portfolio Management with Python.ipynb` — Main notebook with full code and analysis  
- `README.md` — Documentation (this file)

---

## 📦 Requirements

Install dependencies:

```bash
pip install yfinance pandas numpy
```

Optional (for faster experimentation):

```bash
pip install jupyterlab
```

---

## 🧠 Key Concepts Covered

### 1. **Downloading Market Data**
The project uses `yf.download()` to pull historical OHLCV data for each ticker.

### 2. **Understanding MultiIndex Columns**
`yfinance` sometimes returns columns like:

```
('GOOG', 'Close')
('AAPL', 'Close')
```

This requires using tuple‑based indexing instead of typical `df['Close']`.

### 3. **Flattening MultiIndex for Ease**
A utility function converts MultiIndex columns into flat, human‑readable names:

```
('GOOG','Close') → 'GOOG_Close'
```

This dramatically simplifies downstream analysis.

### 4. **Combining Closing Prices**
All assets are merged into a single DataFrame:

```
GOOG | AAPL | META | AMZN | MSFT | GSPC
```

This dataset is ideal for:

- CAPM analysis  
- Portfolio optimization  
- Backtesting  
- Risk modeling  
- Factor analysis  

---

## 🛠 Code Snippet: Extracting Closing Prices

Below is the exact logic used in the notebook:

```python
def flatten_columns(df):
    df.columns = [
        '_'.join(str(c) for c in col) if isinstance(col, tuple) else str(col)
        for col in df.columns
    ]
    return df

GOOG = flatten_columns(GOOG)
AAPL = flatten_columns(AAPL)
META = flatten_columns(META)
AMZN = flatten_columns(AMZN)
MSFT = flatten_columns(MSFT)
GSPC = flatten_columns(GSPC)

dataset = pd.concat([
    GOOG.filter(like="Close"),
    AAPL.filter(like="Close"),
    META.filter(like="Close"),
    AMZN.filter(like="Close"),
    MSFT.filter(like="Close"),
    GSPC.filter(like="Close")
], axis=1)

dataset.columns = ['GOOG','AAPL','META','AMZN','MSFT','GSPC']
```

---

## 📊 What You Can Build on Top of This

Once you have a clean dataset, you can extend the project into:

### ✔ Portfolio optimization (Markowitz, Black‑Litterman)  
### ✔ Risk analysis (volatility, Sharpe, Beta, Alpha)  
### ✔ CAPM & Fama‑French regressions  
### ✔ Rolling correlations & volatility  
### ✔ Backtesting simple trading rules  
### ✔ Factor exposure modeling  

---

## 📝 Author

Dhruv Pant  
Finance & Data Analytics Enthusiast  

---

## ⭐ Contribution

Pull requests are welcome.  
If you find issues or want new features, feel free to open an issue.

---

## 📄 License

This project is licensed under the **MIT License**.

