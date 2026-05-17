Jupyter Notebook ပေါ်မှာ OHLC (Open, High, Low, Close) data တွေကို ဆွဲယူဖို့အတွက် Python ရဲ့ လူသုံးအများဆုံးနဲ့ အဆင်ပြေဆုံးဖြစ်တဲ့ `yfinance` (Yahoo Finance) library ကို အသုံးပြုပြီး အလွယ်တကူ ဆွဲယူနိုင်ပါတယ်။

အောက်ပါအဆင့်များအတိုင်း Jupyter Notebook ထဲမှာ ကုဒ်ရေးသားပြီး လုပ်ဆောင်နိုင်ပါတယ် -

## အဆင့် (၁) လိုအပ်သော Libraries များ ထည့်သွင်းခြင်း

ပထမဆုံး Jupyter Notebook ရဲ့ Cell တစ်ခုထဲမှာ data ဆွဲရန်နှင့် data visual လုပ်ရန်အတွက် လိုအပ်တဲ့ libraries တွေကို အောက်ပါအတိုင်း ရိုက်ထည့်ပြီး Run ပါ။

```bash
!pip install pandas yfinance matplotlib plotly

```

## အဆင့် (၂) Code ရေးသားပြီး OHLC Data ဆွဲယူခြင်း

`yfinance` ဟာ Stock, Crypto ကော Forex Data တွေကိုပါ အခမဲ့ ဆွဲယူခွင့်ပေးပါတယ်။ Notebook cell အသစ်တစ်ခုမှာ အောက်ပါ ကုဒ်ကို ရေးသားပါ။

```python
import yfinance as yf
import pandas as pd

# မိမိ ဆွဲယူလိုသော Financial Instrument ၏ Ticker ကို သတ်မှတ်ပါ 
# (ဥပမာ - Forex အတွက် "EURUSD=X"၊ Crypto အတွက် "BTC-USD"၊ Stock အတွက် "AAPL")
ticker_symbol = "EURUSD=X"

# yf.download() ကို သုံးပြီး သတ်မှတ်ထားတဲ့ ရက်စွဲအလိုက် data ဆွဲယူခြင်း
# interval ကို မိမိလိုအပ်ချက်အပေါ်မူတည်ပြီး '1m', '5m', '1h', '1d', '1wk' စသဖြင့် ပြောင်းလဲနိုင်ပါတယ်
df = yf.download(ticker_symbol, start="2025-01-01", end="2026-01-01", interval="1d")

# ရရှိလာသော DataFrame ၏ ထိပ်ဆုံး row အနည်းငယ်ကို ကြည့်ရှုခြင်း
print(df.head())

```

## အဆင့် (၃) OHLC Data ကို စနစ်တကျ စစ်ဆေးခြင်း

ဆွဲယူလိုက်တဲ့ Data ဟာ Pandas DataFrame format နဲ့ ရောက်ရှိလာမှာ ဖြစ်ပါတယ်။ အကယ်၍ Column တွေထဲကမှ OHLC ကိုပဲ သီးသန့် ခွဲထုတ်ချင်ရင် အောက်ပါအတိုင်း လုပ်ဆောင်နိုင်ပါတယ် -

```python
# OHLC column များကိုသာ သီးသန့် ရွေးထုတ်ခြင်း
ohlc_data = df[['Open', 'High', 'Low', 'Close']]

# အချက်အလက်များ သေချာဝင်၊ မဝင် DataFrame ၏ နောက်ဆုံးအပိုင်းကို စစ်ဆေးခြင်း
print(ohlc_data.tail())

```

---

> **Tip:** အကယ်၍ Live Trading သို့မဟုတ် ပိုမိုတိကျတဲ့ Historical Tick Data တွေအတွက်ဆိုရင် မိမိအသုံးပြုနေတဲ့ Trading Platform (ဥပမာ - MetaTrader 5 Terminal) ကို Python Library ကတစ်ဆင့် ချိတ်ဆက်ပြီးတော့လည်း DataFrame ထဲကို OHLC data တိုက်ရိုက် ဆွဲတင်လို့ ရပါတယ်။

အခု လောလောဆယ် ဘယ်လို Market အမျိုးအစား (Forex, Crypto သို့မဟုတ် Stock) ရဲ့ Data ကို အဓိကထားပြီး ဆွဲယူအသုံးပြုဖို့ စဉ်းစားနေတာလဲခင်ဗျာ?
