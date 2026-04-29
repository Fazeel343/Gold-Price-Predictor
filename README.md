# 🪙 AI Gold Price Predictor

> A machine learning project that forecasts gold prices in both **USD** and **PKR** through 2028, using historical market data, S&P 500 index trends, and the USD-to-PKR exchange rate.

---

## 📌 Project Overview

This project builds a data-driven gold price prediction system trained on 10 years of monthly data (2014–2024). It combines two machine learning models — Linear Regression and Random Forest — with engineered time-series features to forecast gold prices up to December 2028, in both US Dollars and Pakistani Rupees.

---

## 📁 Project Structure

```
gold-price-predictor/
│
├── python.ipynb                  # Main Jupyter Notebook (all blocks)
├── gold_predictor.db             # SQLite database (Gold_Prices + Market_Indicators)
├── monthly.csv                   # Monthly gold price data (USD)
├── sp500_index.csv               # S&P 500 historical index data
├── USD_To_PKR_1947.csv           # USD to PKR exchange rate history
│
├── gold_historical_data.png      # EDA visualization (2014–2024)
├── correlation_matrix.png        # Feature correlation heatmap
└── gold_price_forecast_2028.png  # Final forecast chart (2014–2028)
```

---

## 🗃️ Database Schema

The SQLite database (`gold_predictor.db`) contains two tables:

**`Gold_Prices`**
| Column | Description |
|---|---|
| `Date` | Month (YYYY-MM-DD) |
| `Price` | Gold price in USD/oz |
| `Gold_Price_PKR` | Gold price in PKR/oz |

**`Market_Indicators`**
| Column | Description |
|---|---|
| `Date` | Month (YYYY-MM-DD) |
| `stock_index` | S&P 500 index value |
| `currency_rate` | USD to PKR exchange rate |

---

## ⚙️ How It Works

The notebook is organized into 8 sequential blocks:

1. **Imports & Setup** — Load all libraries and configure the database path
2. **Data Loading** — Read from SQLite, merge tables, and parse dates
3. **Exploratory Data Analysis (EDA)** — Visualize gold prices (USD & PKR) and the exchange rate over time
4. **Feature Engineering** — Create lag features (1-month, 3-month), rolling averages (MA-3, MA-6), and time-based columns
5. **Model Training** — Train and evaluate Linear Regression and Random Forest on an 80/20 split
6. **Future Predictions (2025–2028)** — Iteratively forecast monthly gold prices using estimated PKR depreciation (~0.85 PKR/month) and S&P 500 growth (~3%/year)
7. **Visualization** — Plot historical vs. predicted prices with a ±7% confidence band
8. **Save to Database** — Persist forecast results back into the SQLite database

---

## 🤖 Models Used

| Model | Notes |
|---|---|
| **Linear Regression** | Used for final forecasting (better generalization) |
| **Random Forest** | 200 estimators, max depth 10 — used for comparison |

### Features Fed to the Models

- `Month_Num` — Monotonically increasing month index from Jan 2014
- `Month` — Month of year (seasonality signal)
- `stock_index` — S&P 500 index
- `currency_rate` — USD to PKR rate
- `Price_Lag1`, `Price_Lag3` — Gold price 1 and 3 months prior
- `MA_3`, `MA_6` — 3-month and 6-month rolling averages
- `PKR_Lag1` — Exchange rate from previous month

---

## 📊 Key Findings

- All four features (Gold USD, Gold PKR, S&P 500, Currency Rate) are **highly correlated** — all values ≥ 0.88
- Gold price in PKR has risen dramatically due to both rising USD gold prices and significant PKR depreciation since 2022
- The model forecasts gold reaching approximately **$2,750–$2,800/oz (USD)** and **~860,000–880,000 PKR/oz** by end of 2028

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Run

1. Clone or download the repository
2. Open `python.ipynb` in Jupyter Notebook or JupyterLab
3. Update `DB_PATH` in Block 1 to point to your local `gold_predictor.db`
4. Run all cells in order (Kernel → Restart & Run All)

---

## 📈 Output Visualizations

| Chart | Description |
|---|---|
| `gold_historical_data.png` | Three-panel EDA: Gold (USD), Gold (PKR), and USD/PKR rate from 2014–2024 |
| `correlation_matrix.png` | Heatmap showing feature correlations |
| `gold_price_forecast_2028.png` | Side-by-side forecast in USD and PKR with confidence bands |

---

## ⚠️ Limitations & Disclaimer

- Predictions assume stable linear PKR depreciation and moderate S&P 500 growth — sudden economic shocks are not modeled
- The ±7% confidence band is manually set, not derived from model uncertainty
- This project is built for **academic purposes only** and should not be used as financial advice

---

## 📜 License

This project is licensed under the MIT License. 
