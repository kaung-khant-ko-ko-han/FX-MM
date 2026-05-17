OHLC (Open, High, Low, Close) ဒေတာတွေကို Jupyter Notebook ထဲ ဆွဲယူဖို့ နည်းလမ်းများစွာ ရှိပါတယ်။ အဓိက သုံးတဲ့ နည်းလမ်းတွေကတော့ –

1. **Python library သုံးပြီး အွန်လိုင်းကနေ တိုက်ရိုက်ဆွဲယူခြင်း** (ဥပမာ `yfinance`, `pandas_datareader`)  
2. **CSV ဖိုင်ကနေ ဖတ်ယူခြင်း**  

အောက်မှာ တစ်ခုချင်းစီကို ဥပမာ code နဲ့တကွ ရှင်းပြပေးပါမယ်။

---

## ၁။ yfinance သုံးပြီး Yahoo Finance မှ ဆွဲယူခြင်း (အလွယ်ဆုံး)

`yfinance` က Yahoo Finance ရဲ့ data ကို အလွယ်တကူ ဆွဲထုတ်ပေးပါတယ်။

### ထည့်သွင်းရန်
```python
!pip install yfinance
```

### အသုံးပြုပုံ
```python
import yfinance as yf

# ဥပမာ - Apple (AAPL) ရဲ့ ၁ နှစ်စာ နေ့စဉ် OHLC data
ticker = "AAPL"
data = yf.download(ticker, period="1y", interval="1d")  # 1 day interval

# data ထဲမှာ Open, High, Low, Close, Adj Close, Volume ပါမယ်
print(data.head())
```

**Parameter တွေ**  
- `period`: "1d", "5d", "1mo", "3mo", "6mo", "1y", "2y", "5y", "10y", "ytd", "max"  
- `interval`: "1m", "2m", "5m", "15m", "30m", "60m", "90m", "1h", "1d", "5d", "1wk", "1mo", "3mo"

ဥပမာ – မိနစ် ၁၅ ကြား data
```python
data = yf.download(ticker, period="5d", interval="15m")
```

---

## ၂။ pandas_datareader သုံးခြင်း

`pandas_datareader` က Yahoo, Google, FRED စတဲ့ source အမျိုးမျိုးကနေ data ဆွဲနိုင်ပါတယ်။

### ထည့်သွင်းရန်
```python
!pip install pandas_datareader
```

### အသုံးပြုပုံ
```python
import pandas_datareader.data as web
import datetime

start = datetime.datetime(2023, 1, 1)
end = datetime.datetime(2023, 12, 31)

# Yahoo Finance မှ 'AAPL' ဆွဲမယ်
data = web.DataReader('AAPL', 'yahoo', start, end)
print(data.head())
```

---

## ၃။ CSV ဖိုင်မှ ဖတ်ခြင်း

သင့်မှာ OHLC data တွေ CSV format နဲ့ ရှိရင် `pandas` နဲ့ အလွယ်တကူ ဖတ်လို့ရပါတယ်။

```python
import pandas as pd

# ဖိုင်ကို ဖတ်မယ်
data = pd.read_csv('ohlc_data.csv')

# Date column ကို datetime အဖြစ်ပြောင်း၊ index လုပ်ချင်ရင်
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

print(data.head())
```

CSV ဖိုင်ထဲမှာ အနည်းဆုံး `Date`, `Open`, `High`, `Low`, `Close` ဆိုတဲ့ column တွေပါသင့်တယ်။

---

## ၄။ ဆွဲယူပြီးရင် Visualization လုပ်ခြင်း

OHLC data ကို candlestick chart နဲ့ ကြည့်ချင်ရင် `mplfinance` သုံးလို့ရပါတယ်။

### ထည့်သွင်းရန်
```python
!pip install mplfinance
```

### Candlestick ဆွဲခြင်း
```python
import mplfinance as mpf

# data က yfinance ကနေရတဲ့ DataFrame
mpf.plot(data, type='candle', style='charles', volume=True, title='AAPL Candlestick')
```

`plotly` သုံးပြီး interactive chart လည်းလုပ်နိုင်ပါတယ်။

---

## အရေးကြီးမှတ်ချက်
- Yahoo Finance က data အခမဲ့ရပေမယ့် တစ်ခါတစ်ရံ rate limit ရှိနိုင်တယ်။ `yfinance` ကို နောက်ဆုံး version ဖြစ်အောင် update လုပ်ပေးပါ။  
- `pandas_datareader` က Yahoo API အပြောင်းအလဲကြောင့် တစ်ခါတစ်ရံ အလုပ်မလုပ်တာဖြစ်နိုင်လို့ `yfinance` ကိုပဲ အကြံပြုချင်ပါတယ်။

ဒီနည်းတွေနဲ့ Jupyter Notebook ထဲမှာ OHLC data တွေ အလွယ်တကူ ဆွဲယူပြီး ခွဲခြမ်းစိတ်ဖြာနိုင်ပါပြီ။ နောက်ထပ်သိချင်တာရှိရင် မေးနိုင်ပါတယ်။
