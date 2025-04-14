

```markdown
# 📈 Stock Price Forecasting using Facebook Prophet

This project demonstrates how to fetch historical stock data using Yahoo Finance (`yfinance`) and generate future forecasts using [Facebook Prophet](https://facebook.github.io/prophet/). It includes data preprocessing, visualization, and forecasting logic using the additive time series model.

---

## 🚀 Features

- Fetches historical stock data from Yahoo Finance
- Uses Facebook Prophet for time series forecasting
- Handles missing data and outliers robustly
- Visualizes historical and predicted stock prices
- Easily customizable for any stock ticker symbol

---

## 🛠️ Installation

Install the required packages using `pip`:

```bash
pip install prophet yfinance
```

> Note: `prophet` may require dependencies such as `cmdstanpy`, `matplotlib`, `pandas`, etc., which are automatically installed with the above command.

---

## 📊 Data Source

- Stock market data is fetched from Yahoo Finance using the `yfinance` package.
- Example ticker symbols:  
  - `ABAT` (used in this repo)  
  - `^GSPC` (S&P 500)  
  - Any other valid Yahoo Finance ticker

---

## 🧪 How It Works

1. **Data Fetching**  
   Historical stock data is downloaded using the `yfinance` package with `auto_adjust=True` to reflect stock splits and dividends.

2. **Preprocessing**  
   - Only the "Close" price is selected for forecasting.
   - Data is reformatted to match Prophet’s requirements (`ds` and `y` columns).

3. **Forecasting**  
   - Prophet models seasonality, trend changes, and holidays.
   - Forecast horizon and plot customization are available.

---

## 📂 Usage

Run the main script to:
- Fetch historical stock data
- Preprocess the data
- Train the Prophet model
- Plot the forecast

```python
from prophet import Prophet
import yfinance as yf
import pandas as pd
from datetime import timedelta

# Parameters
stock = 'ABAT'
start = '1900-01-01'
end = pd.to_datetime("today") - timedelta(days=1)

# Load and prepare data
df = yf.download(stock, start=start, end=end, auto_adjust=True)
df = df[['Close']].reset_index()
df.rename(columns={'Date': 'ds', 'Close': 'y'}, inplace=True)

# Model and forecast
model = Prophet()
model.fit(df)
future = model.make_future_dataframe(periods=365)
forecast = model.predict(future)

# Plot
fig = model.plot(forecast)
```

---

## 📌 Requirements

- Python 3.7+
- prophet 1.1.6
- yfinance 0.2.48
- pandas
- matplotlib

---

## 📷 Sample Output

![Forecast Plot Example](docs/forecast_sample.png)  
_Forecast plot including historical data, predicted trend, and uncertainty intervals._

---

## 📎 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change or improve.

---

## 🙋‍♀️ Acknowledgements

- [Facebook Prophet](https://github.com/facebook/prophet)
- [Yahoo Finance](https://finance.yahoo.com/)
- [yfinance](https://github.com/ranaroussi/yfinance)

---
```



