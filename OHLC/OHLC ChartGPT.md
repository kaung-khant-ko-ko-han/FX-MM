Jupyter Notebook ပေါ်မှာ OHLC (Open, High, Low, Close) data ကို ဆွဲယူဖို့ Python library တွေကို အသုံးပြုနိုင်ပါတယ်။ အများဆုံးအသုံးများတာတွေက —

* Yahoo Finance (`yfinance`)
* Binance API (`ccxt`)
* MetaTrader5 Python API
* Alpha Vantage
* Polygon.io

အောက်မှာ အလွယ်ဆုံးနည်းဖြစ်တဲ့ `yfinance` နဲ့ Binance (`ccxt`) ဥပမာတွေပြထားပါတယ်။

---

# 1. Yahoo Finance မှ OHLC Data ဆွဲယူခြင်း

## Install

Jupyter Notebook cell ထဲမှာ run ပါ။

```python
!pip install yfinance pandas
```

---

## Example Code

```python
import yfinance as yf
import pandas as pd

# Symbol
symbol = "AAPL"

# Download OHLC Data
df = yf.download(
    symbol,
    start="2025-01-01",
    end="2025-05-01",
    interval="1d"
)

# Show Data
print(df.head())
```

---

## Output Example

| Date       | Open | High | Low | Close | Volume |
| ---------- | ---- | ---- | --- | ----- | ------ |
| 2025-01-02 | ...  | ...  | ... | ...   | ...    |

---

# 2. Binance Crypto OHLC Data (ccxt)

Crypto trading data အတွက် အသုံးများပါတယ်။

## Install

```python
!pip install ccxt pandas
```

---

## Example

```python
import ccxt
import pandas as pd

exchange = ccxt.binance()

# Fetch OHLCV
bars = exchange.fetch_ohlcv(
    'BTC/USDT',
    timeframe='1h',
    limit=100
)

# Convert to DataFrame
df = pd.DataFrame(
    bars,
    columns=['timestamp', 'open', 'high', 'low', 'close', 'volume']
)

# Convert timestamp
df['timestamp'] = pd.to_datetime(df['timestamp'], unit='ms')

print(df.head())
```

---

# 3. Candlestick Chart ဆွဲခြင်း

OHLC data ကို chart ပြချင်ရင် `mplfinance` သုံးနိုင်ပါတယ်။

## Install

```python
!pip install mplfinance
```

---

## Example

```python
import mplfinance as mpf

# Yahoo Finance data already loaded in df
mpf.plot(
    df,
    type='candle',
    volume=True,
    style='yahoo'
)
```

---

# 4. MetaTrader 5 ကနေ Direct OHLC Data ယူခြင်း

MT5 install လုပ်ထားရင် Python API နဲ့ တိုက်ရိုက်ဆွဲနိုင်ပါတယ်။

## Install

```python
!pip install MetaTrader5
```

---

## Example

```python
import MetaTrader5 as mt5
import pandas as pd

# Connect MT5
mt5.initialize()

# Get Rates
rates = mt5.copy_rates_from_pos(
    "EURUSD",
    mt5.TIMEFRAME_H1,
    0,
    100
)

# Convert DataFrame
df = pd.DataFrame(rates)

# Convert time
df['time'] = pd.to_datetime(df['time'], unit='s')

print(df.head())
```

---

# Beginner အတွက် Recommendation

| Source          | Best For             |
| --------------- | -------------------- |
| `yfinance`      | Stock Data           |
| `ccxt`          | Crypto Exchange      |
| `MetaTrader5`   | Forex + MT5          |
| `Alpha Vantage` | Free API             |
| `Polygon`       | Professional Trading |

---

# Data Analysis Example

OHLC data ရပြီးရင် —

* Moving Average
* RSI
* MACD
* AI/ML Prediction
* Candlestick Pattern Detection
* Backtesting

တွေ ဆက်လုပ်နိုင်ပါတယ်။

ဥပမာ SMA:

SMA = \frac{P_1 + P_2 + \cdots + P_n}{n}

```python
df['SMA20'] = df['Close'].rolling(20).mean()
```

---

Jupyter Notebook ကို TradingView လို Candlestick + Indicators + Real-time OHLC Scanner အဖြစ် setup လုပ်ချင်ရင်လည်း ဆက်ရှင်းပြပေးနိုင်ပါတယ်။
