

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

သင်ပေးပို့ထားသော လင့်ခ်သည် **MetaTrader 5 (MT5) အတွက် Python Package** ၏ တရားဝင် စာရွက်စာတမ်းဖြစ်ပါသည်။ ၎င်းသည် MT5 terminal မှ ဈေးနှုန်းဒေတာ၊ ကုန်သွယ်မှုမှတ်တမ်းများနှင့် အကောင့်အချက်အလက်များကို Python ဖြင့် တိုက်ရိုက်ရယူရန် အသုံးပြုသည့် module တစ်ခုဖြစ်သည်။

အောက်တွင် OHLC ဒေတာ ထုတ်ယူနည်းကို အဓိကထား၍ အကျဉ်းချုံး ဖော်ပြထားပါသည်။

---

## MetaTrader5 Python Package အသုံးပြု၍ OHLC ဒေတာ ထုတ်ယူနည်း

**MetaTrader5** Python package သည် MT5 terminal သို့ ချိတ်ဆက်ပြီး အောက်ပါတို့ကို လုပ်ဆောင်နိုင်သည်-
- သမိုင်းဝင် OHLC (Open, High, Low, Close) ဒေတာ ရယူခြင်း
- Tick ဒေတာ ရယူခြင်း
- ကုန်သွယ်မှု အမိန့်များ ပေးပို့ခြင်း
- အကောင့်အချက်အလက် ကြည့်ရှုခြင်း

### 1. Package ထည့်သွင်းခြင်း

```bash
pip install MetaTrader5
```

### 2. MT5 Terminal သို့ ချိတ်ဆက်ခြင်း

```python
import MetaTrader5 as mt5

# MT5 terminal ကို စတင်ပြီး ချိတ်ဆက်ခြင်း (ဖွင့်ထားရန် လိုအပ်)
if not mt5.initialize():
    print("MT5 ချိတ်ဆက်မှု မအောင်မြင်ပါ၊ အမှားကုဒ်:", mt5.last_error())
    quit()
```

### 3. OHLC ဒေတာ ရယူရန် အဓိက Functions များ

| Function | ရှင်းလင်းချက် | အသုံးပြုပုံ |
| :--- | :--- | :--- |
| `mt5.copy_rates_from(symbol, timeframe, from_date, count)` | သတ်မှတ်ထားသော ရက်စွဲမှစ၍ အတိတ်ဘက်သို့ bar အရေအတွက်ကို ရယူသည်။ | `rates = mt5.copy_rates_from("EURUSD", mt5.TIMEFRAME_H1, datetime(2025,5,1), 100)` |
| `mt5.copy_rates_from_pos(symbol, timeframe, start_pos, count)` | terminal ရှိ လက်ရှိဒေတာဘေ့စ်ထဲမှ စတင်ရန် အနေအထား (index) ကို သတ်မှတ်ပြီး bar များ ရယူသည်။ | `rates = mt5.copy_rates_from_pos("EURUSD", mt5.TIMEFRAME_H1, 0, 200)` |
| `mt5.copy_rates_range(symbol, timeframe, date_from, date_to)` | ရက်စွဲအကွာအဝေးအတွင်း bar များ အားလုံးကို ရယူသည်။ | `rates = mt5.copy_rates_range("EURUSD", mt5.TIMEFRAME_D1, datetime(2025,4,1), datetime(2025,5,1))` |

အထက်ပါ function များသည် `numpy` array တစ်ခုကို ပြန်ပေးပြီး column တစ်ခုချင်းစီမှာ `time`, `open`, `high`, `low`, `close`, `tick_volume`, `spread`, `real_volume` တို့ဖြစ်သည်။

### 4. နမူနာ – နေ့စဉ် OHLC ဒေတာ ရယူခြင်း

```python
import MetaTrader5 as mt5
from datetime import datetime

# MT5 နှင့်ချိတ်ဆက်
mt5.initialize()

# Symbol နှင့် Timeframe သတ်မှတ်
symbol = "EURUSD"
timeframe = mt5.TIMEFRAME_D1  # နေ့စဉ်

# 2025 ခုနှစ် ဇန်နဝါရီ ၁ ရက်မှ မေလ ၁ ရက်အထိ ဒေတာ ရယူ
rates = mt5.copy_rates_range(symbol, timeframe,
                               datetime(2025, 1, 1),
                               datetime(2025, 5, 1))

# OHLC ဒေတာကို ပြသခြင်း
print("စုစုပေါင်း bar အရေအတွက်:", len(rates))
for bar in rates[:5]:  # ပထမ ၅ ခုသာ ပြရန်
    print(datetime.utcfromtimestamp(bar['time']), 
          "O:", bar['open'], 
          "H:", bar['high'], 
          "L:", bar['low'], 
          "C:", bar['close'])
```

**Output (ဥပမာ)**:
```
2025-01-02 00:00:00 O: 1.03521 H: 1.03789 L: 1.02700 C: 1.03123
2025-01-03 00:00:00 O: 1.03120 H: 1.03657 L: 1.02818 C: 1.03545
...
```

### 5. MT5 Terminal နှင့် ချိတ်ဆက်မှု ဖြုတ်ခြင်း

```python
mt5.shutdown()
```

### 6. အရေးကြီးမှတ်ချက်
- ဤ module ကို အသုံးပြုရန် MT5 terminal ကို သင့်ကွန်ပျူတာတွင် ဖွင့်ထားရန် လိုအပ်ပြီး အနည်းဆုံး **Demo** အကောင့်တစ်ခု ရှိရပါမည်။
- `initialize()` မခေါ်မီ terminal ကို စတင်ထားရန် သို့မဟုတ် `mt5.initialize(path="terminal_path")` ဖြင့် terminal ကို အလိုအလျောက် ဖွင့်ခိုင်းနိုင်သည်။
- OHLC ဒေတာအပြင် Tick ဒေတာများ ရယူရန် `mt5.copy_ticks_from()` နှင့် `mt5.copy_ticks_range()` function များ ရှိပါသည်။

အသေးစိတ်ကို မူရင်း [MetaTrader 5 Python Package စာရွက်စာတမ်း](https://www.mql5.com/en/docs/python_metatrader5) တွင် ဖတ်ရှုနိုင်ပါသည်။
