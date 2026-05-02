# ZAR/USD Exchange Rate Forecasting

A multi-model econometric forecasting pipeline for the South African rand (ZAR/USD),
built using monthly macroeconomic data from the FRED database (1987–2013).

## Models Compared
| Model | Description |
|---|---|
| ARIMA | Baseline autoregressive model, order selected via AIC |
| ARIMAX | ARIMA extended with interest rate differential and oil returns as regressors |
| GARCH(1,1) | Volatility model capturing heteroskedasticity in log-returns |
| Ensemble | Equal-weight combination of ARIMA and GARCH mean forecasts |

## Key Findings
- ZAR log-returns exhibit near-random-walk behaviour at monthly frequency,
  consistent with the efficient market hypothesis for emerging market currencies.
- ARCH effects were not statistically significant at monthly frequency (ARCH-LM p=0.97),
  a meaningful econometric result in itself.
- The interest rate differential (US Fed Funds rate minus SA repo rate) and Brent crude
  oil returns served as external regressors in the ARIMAX specification.

## Methodology
1. Data ingestion from FRED API — USD/ZAR, SA repo rate, US Fed Funds rate, Brent crude
2. Log-return transformation and ADF stationarity testing
3. ACF/PACF diagnostics and ARCH-LM heteroskedasticity testing
4. Model fitting — ARIMA, ARIMAX, GARCH(1,1), Ensemble
5. Walk-forward rolling validation
6. Evaluation via MAE, RMSE, MAPE and the Diebold-Mariano test

## Tech Stack
Python · Pandas · NumPy · statsmodels · pmdarima · arch · Matplotlib

## How to Run
```bash
pip install pandas numpy matplotlib statsmodels pmdarima arch
jupyter notebook ZAR_Forecasting.ipynb
```

## Data Source
All data sourced from the [FRED database](https://fred.stlouisfed.org/) (Federal Reserve Bank of St. Louis).
No manual downloads required — data is pulled directly via URL in the notebook.
