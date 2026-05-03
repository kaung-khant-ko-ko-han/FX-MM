`smartmoneyconcepts` ဆိုတာ Inner Circle Trader (ICT) ရဲ့ Smart Money Concepts (SMC) ကို Python နဲ့ algorithmic trading အတွက် အကောင်အထည်ဖော်ထားတဲ့ package တစ်ခုပါ။ ဒီ package ကို သုံးပြီး စျေးကွက်ဖွဲ့စည်းပုံ (market structure)၊ order blocks၊ fair value gaps စတာတွေကို ရှာဖွေနိုင်ပြီး၊ ရလဒ်တွေကို matplotlib နဲ့ ပြန်မြင်ယောင်နိုင်ပါတယ်။

---
## ၁။ Installation

အောက်ပါ command ကို terminal မှာ run ပြီး install လုပ်နိုင်ပါတယ်။

```bash
pip install smartmoneyconcepts
```

> **မှတ်ချက်** - PyPI မှာ `smartmoneyconcepts` နဲ့ `smart-money-concept` ဆိုပြီး မတူညီတဲ့ package နှစ်ခုရှိပါတယ်။ ဒီစာမျက်နှာမှာ ရှင်းပြထားတာ `smartmoneyconcepts` (leero-ady ထုတ်ဝေတဲ့) အကြောင်းပါ။

---
## ၂။ အခြေခံအသုံးပြုနည်း

### ၂.၁ ဒေတာပြင်ဆင်ခြင်း

smc က **Pandas DataFrame** ကို လက်ခံပါတယ်။ အောက်ပါအတိုင်း Column name တွေကို စာလုံးသေးနဲ့ ထားရပါမယ်။

```python
import pandas as pd
from smartmoneyconcepts import smc

# OHLCV ဒေတာ ပြင်ဆင်ပါ
data = {
    "open":  [100, 101, 102, 103, 104],
    "high":  [105, 106, 107, 108, 109],
    "low":   [95, 96, 97, 98, 99],
    "close": [101, 102, 103, 104, 105],
    "volume":[1000, 1100, 1200, 1300, 1400]
}
df = pd.DataFrame(data)
```

### ၂.၂ Indicator တွေ တွက်ချက်ခြင်း

```python
# FVG တွက်မယ်
fvg = smc.fvg(df)

# Swing Highs/Lows တွက်မယ်
swing = smc.swing_highs_lows(df, swing_length=50)

# BOS & CHoCH တွက်မယ် (swing data လိုတယ်)
bos_choch = smc.bos_choch(df, swing, close_break=True)

# Order Blocks တွက်မယ်
ob = smc.ob(df, swing, close_mitigation=False)

# Liquidity တွက်မယ်
liquidity = smc.liquidity(df, swing)
```

---
## ၃။ Indicator တစ်ခုချင်းစီရဲ့ အသေးစိတ်

### ၃.၁ Fair Value Gap (FVG) - `smc.fvg()`

**သဘောတရား** - စျေးကွက်မှာ ကွာဟချက် (gap) ဖြစ်ပေါ်တာကို ရှာပါတယ်။ Bullish FVG ဆိုရင် ယခင် candle ရဲ့ high က နောက် candle ရဲ့ low ထက် နိမ့်နေတာ၊ Bearish FVG ဆိုရင် ယခင် candle ရဲ့ low က နောက် candle ရဲ့ high ထက် မြင့်နေတာကို ဆိုလိုပါတယ်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `join_consecutive` | bool | `True` ဆို FVG တွေ ဆက်တိုက်ရှိနေရင် ပေါင်းစည်းပေးမယ် |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `FVG` | 1 = Bullish, -1 = Bearish |
| `Top` | FVG ရဲ့ အပေါ်ဆုံးအမှတ် |
| `Bottom` | FVG ရဲ့ အောက်ဆုံးအမှတ် |
| `MitigatedIndex` | FVG ပြန်ဖြည့်တဲ့ candle index |

### ၃.၂ Swing Highs and Lows - `smc.swing_highs_lows()`

**သဘောတရား** - Swing High ဆိုတာ သတ်မှတ်ထားတဲ့ candle အရေအတွက် (swing_length) ရဲ့ အရှေ့နဲ့အနောက်မှာ အမြင့်ဆုံး high ဖြစ်နေတာပါ။ Swing Low ကတော့ အနိမ့်ဆုံး low ဖြစ်နေတာပါ။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `swing_length` | int | အရှေ့နဲ့အနောက် ဘယ်လောက် candle ကြည့်မလဲ (default: 50) |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `HighLow` | 1 = Swing High, -1 = Swing Low |
| `Level` | Swing point ရဲ့ စျေးနှုန်း |

### ၃.၃ Break of Structure (BOS) & Change of Character (CHoCH) - `smc.bos_choch()`

**သဘောတရား** - BOS ဆိုတာ လက်ရှိ trend အတိုင်း ဆက်သွားတာကို အတည်ပြုတဲ့ structural break ဖြစ်ပြီး၊ CHoCH ကတော့ trend ပြောင်းသွားတာကို ညွှန်ပြတဲ့ break ဖြစ်ပါတယ်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `swing_highs_lows` | DataFrame | `swing_highs_lows()` က return |
| `close_break` | bool | `True` ဆို candle close နဲ့ break ကို စစ်မယ် |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `BOS` | 1 = Bullish, -1 = Bearish |
| `CHOCH` | 1 = Bullish, -1 = Bearish |
| `Level` | Break ဖြစ်တဲ့ စျေးနှုန်းအဆင့် |
| `BrokenIndex` | Break ဖြစ်တဲ့ candle index |

### ၃.၄ Order Blocks (OB) - `smc.ob()`

**သဘောတရား** - စျေးကွက်မှာ အမှာစာတွေ အများအပြားစုနေတဲ့ စျေးနှုန်းအကွာအဝေးကို Order Block အနေနဲ့ သတ်မှတ်ပါတယ်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `swing_highs_lows` | DataFrame | `swing_highs_lows()` က return |
| `close_mitigation` | bool | `True` ဆို candle close နဲ့ mitigate ကို စစ်မယ် |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `OB` | 1 = Bullish, -1 = Bearish |
| `Top` | Order block ရဲ့ အပေါ်ဆုံး |
| `Bottom` | Order block ရဲ့ အောက်ဆုံး |
| `OBVolume` | Volume + နောက်ဆုံး volume ၂ ခု |
| `Percentage` | Order block ရဲ့ အားကောင်းမှု % |

### ၃.၅ Liquidity - `smc.liquidity()`

**သဘောတရား** - High တွေ (သို့) Low တွေ တစ်ခုနဲ့တစ်ခု အနီးကပ်ရှိနေတဲ့အခါ Liquidity zone အဖြစ် သတ်မှတ်ပါတယ်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `range_percent` | float | Liquidity အဖြစ်သတ်မှတ်မယ့် % range |

---
## ၄။ လက်တွေ့အသုံးချနည်းများ

### ၄.၁ FVG နဲ့ Trading Signal

```python
fvg_result = smc.fvg(df)
if fvg_result['FVG'].iloc[-1] == 1:
    print("Bullish FVG → Buy Signal")
elif fvg_result['FVG'].iloc[-1] == -1:
    print("Bearish FVG → Sell Signal")
```


### ၄.၂ Swing High/Low နဲ့ Trend Analysis

```python
swing = smc.swing_highs_lows(df, swing_length=50)
if swing['HighLow'].iloc[-1] == 1:
    print("Uptrend")
elif swing['HighLow'].iloc[-1] == -1:
    print("Downtrend")
```


---
## ၅။ MT5 နဲ့ ပေါင်းစပ်အသုံးပြုခြင်း

MetaTrader 5 ကနေ OHLC data ကို Python နဲ့ ဆွဲထုတ်ပြီး `smartmoneyconcepts` နဲ့ SMC indicator တွေ တွက်ချက်နိုင်ပါတယ်။

```python
import MetaTrader5 as mt5
import pandas as pd
from smartmoneyconcepts import smc

# MT5 ကို ချိတ်ဆက်ပါ
mt5.initialize()

# OHLC data ဆွဲထုတ်ပါ
rates = mt5.copy_rates_from_pos("EURUSD", mt5.TIMEFRAME_H1, 0, 500)
df = pd.DataFrame(rates)
df.columns = ["time", "open", "high", "low", "close", "tick_volume", "spread", "real_volume"]
df = df[["open", "high", "low", "close", "tick_volume"]]
df.rename(columns={"tick_volume": "volume"}, inplace=True)

# SMC indicator တွေ တွက်ပါ
fvg = smc.fvg(df)
swing = smc.swing_highs_lows(df, swing_length=50)
bos_choch = smc.bos_choch(df, swing)
ob = smc.ob(df, swing)

mt5.shutdown()
```

---
## ၆။ အားသာချက်များနှင့် ကန့်သတ်ချက်များ

| အားသာချက် | ကန့်သတ်ချက် |
|------------|--------------|
| Pure Python ဖြစ်လို့ install လုပ်ရလွယ် | FVG, Swing High/Low, OB, BOS/CHoCH, Liquidity ဆိုတဲ့ indicator ၅ မျိုးပဲ ပါသေးတယ် |
| Pandas DataFrame နဲ့ အလုပ်လုပ်လို့ data manipulation လွယ် | Live/real-time data support မပါသေးဘူး |
| Open source (MIT License) ဖြစ်လို့ လွတ်လပ်စွာ သုံးနိုင်၊ ပြင်ဆင်နိုင် | Documentation အနည်းငယ်သာ ရှိသေးတယ် |
| ICT Concept တွေကို Python ecosystem ထဲ သယ်ဆောင်လာ | Backtesting framework မပါဝင်သေးဘူး |

---
## ၇။ အခြားရွေးချယ်စရာ Package များ

| Package | ထူးခြားချက် |
|---------|-------------|
| `smart-money-concept` | Visualization နဲ့ CLI ပါတယ်၊ yfinance ကနေ data တိုက်ရိုက်ဆွဲနိုင် |
| `smc-toolkit` | Vectorized ဖြစ်လို့ မြန်ဆန်၊ Quantitative analysis အတွက် သင့်တော် |

---
## ၈။ အကျဉ်းချုပ်

`smartmoneyconcepts` ဟာ ICT ရဲ့ Smart Money Concepts တွေကို Python နဲ့ အလွယ်တကူ တွက်ချက်နိုင်ဖို့ ရည်ရွယ်ထားတဲ့ package တစ်ခုပါ။ OHLCV data ကို Pandas DataFrame အနေနဲ့ ထည့်ပေးရုံနဲ့ FVG, Swing High/Low, BOS/CHoCH, Order Blocks, Liquidity စတဲ့ indicator တွေကို ချက်ချင်းတွက်ချက်နိုင်ပါတယ်။

algorithmic trading အတွက် SMC approach ကို Python မှာ စမ်းသပ်ချင်သူတွေ၊ ICT concept တွေကို automated trading system မှာ ထည့်သုံးချင်သူတွေအတွက် ဒီ package က အစပြုဖို့ ကောင်းမွန်တဲ့ နေရာတစ်ခု ဖြစ်ပါတယ်။



---

ဟုတ်ကဲ့၊ အခု သင်ပေးပို့ထားတဲ့ **joshyattridge/smart-money-concepts** GitHub repository အကြောင်းကို အသေးစိတ်ရှင်းပြပါမယ်။ ဒီ repository ဟာ ခုနက PyPI က `smartmoneyconcepts` package ရဲ့ Source Code တည်ရှိရာ နေရာဖြစ်ပြီး၊ အဲ့ဒီ package မှာ မပါဝင်သေးတဲ့ indicator အပိုတွေလည်း ထည့်သွင်းထားပါတယ်။

---
## ၁။ Repository အကျဉ်းချုပ်

| အကြောင်းအရာ | အသေးစိတ် |
|---------------|------------|
| Repository အမည် | `joshyattridge/smart-money-concepts` |
| ဖန်တီးသူ | Josh Attridge (GitHub: `joshyattridge`, PyPI: `leero-ady`) |
| ရည်ရွယ်ချက် | ICT ၏ Smart Money Concepts ကို Python ဖြင့် Algorithmic Trading ပြုလုပ်ရန် |
| ပရိုဂရမ်ဘာသာစကား | Python 100% |
| လိုင်စင် | MIT License |
| Star အရေအတွက် | 138 (joshyattridge repo) / 772 (leero-ady repo) |
| Fork အရေအတွက် | 83 / 426 |
| Repository အရွယ်အစား | 23.1 MB |
| နောက်ဆုံး Update | ၂ လခန့် (2026 ခုနှစ်အစောပိုင်း) |

Repository နှစ်ခုရှိတာကတော့ `joshyattridge/smart-money-concepts` က မူရင်းဖြစ်ပြီး `leero-ady/smart-money-concepts` က PyPI package နဲ့ချိတ်ဆက်ထားတဲ့ mirror/fork repository ဖြစ်ပါတယ်။ နှစ်ခုစလုံးက တူညီတဲ့ source code ကို ကိုယ်စားပြုပါတယ်။

---
## ၂။ Repository ဖွဲ့စည်းပုံ

Repository ထဲမှာ အောက်ပါအတိုင်း ဖိုင်တွေနဲ့ ဖိုင်တွဲတွေ ပါဝင်ပါတယ်။

```
smart-money-concepts/
├── smc.py                  # အဓိက indicator အားလုံးပါဝင်သော core module
├── smc/
│   └── __init__.py         # Package init file
├── tests/                  # Unit tests များ
├── setup.py                # Package installation setup
├── README.md               # အသုံးပြုနည်းလမ်းညွှန်
├── LICENSE                 # MIT License
└── .gitignore              # Git မှ ချန်လှပ်ရမည့်ဖိုင်များ
```

`smc.py` ဖိုင်တစ်ခုတည်းမှာ indicator အားလုံးကို function တွေအဖြစ် အကောင်အထည်ဖော်ထားပြီး၊ `iloc` ကို အသုံးပြုကာ high/low values တွေကို ပိုမိုတိကျစွာ ကိုင်တွယ်နိုင်အောင် ပြုလုပ်ထားပါတယ်။

---
## ၃။ PyPI Package နှင့် ကွာခြားချက် - အပို Indicator ၃ ခု

PyPI စာမျက်နှာမှာ ဖော်ပြထားတဲ့ FVG, Swing Highs/Lows, BOS/CHoCH, Order Blocks, Liquidity ဆိုတဲ့ indicator ၅ ခုအပြင် GitHub repository ရဲ့ README မှာ နောက်ထပ် indicator ၃ ခု ထပ်တိုးပါဝင်ပါတယ်။

### ၃.၁ Previous High and Low - `smc.previous_high_low()`

**သဘောတရား** - သတ်မှတ်ထားသော timeframe တစ်ခု၏ ယခင် high နှင့် low တန်ဖိုးများကို ပြန်လည်ရယူပေးပါသည်။ စျေးနှုန်းက ၎င်းအဆင့်များကို ကျော်ဖြတ်သွားခြင်း ရှိမရှိကိုလည်း စစ်ဆေးပေးပါသည်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `ohlc` | DataFrame | OHLC ဒေတာ |
| `time_frame` | str | ယခင် high/low ရယူမည့် timeframe (`"15m"`, `"1H"`, `"4H"`, `"1D"`, `"1W"`, `"1M"`) |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `PreviousHigh` | ယခင် timeframe ၏ အမြင့်ဆုံးစျေးနှုန်း |
| `PreviousLow` | ယခင် timeframe ၏ အနိမ့်ဆုံးစျေးနှုန်း |
| `BrokenHigh` | စျေးနှုန်းက ယခင် high ကို ကျော်သွားလျှင် 1၊ မဟုတ်လျှင် 0 |
| `BrokenLow` | စျေးနှုန်းက ယခင် low ကို ကျော်သွားလျှင် 1၊ မဟုတ်လျှင် 0 |

> **အသုံးပြုပုံ** - Daily, Weekly, Monthly High/Low တွေကို Support/Resistance အဖြစ် သုံးပြီး Breakout trading ပြုလုပ်ရာမှာ အသုံးဝင်ပါတယ်။

### ၃.၂ Sessions - `smc.sessions()`

**သဘောတရား** - သတ်မှတ်ထားသော trading session အတွင်း ရောက်ရှိနေသည့် candle များကို ဖော်ထုတ်ပေးပြီး၊ ထို session ၏ high နှင့် low ကို တွက်ချက်ပေးပါသည်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `ohlc` | DataFrame | OHLC ဒေတာ |
| `session` | str | Trading session အမည် |
| `start_time` | str | Custom session အတွက် စတင်ချိန် (`"HH:MM"` format) |
| `end_time` | str | Custom session အတွက် ပြီးဆုံးချိန် (`"HH:MM"` format) |
| `time_zone` | str | Candle များ၏ time zone (`"UTC+0"` သို့မဟုတ် `"GMT+0"` format) |

**ရရှိနိုင်သော Session အမည်များ:**

| Session အမည် | အကျုံးဝင်သည့်အချိန် |
|---------------|----------------------|
| `"Sydney"` | ဆစ်ဒနီစျေးကွက်ဖွင့်ချိန် |
| `"Tokyo"` | တိုကျိုစျေးကွက်ဖွင့်ချိန် |
| `"London"` | လန်ဒန်စျေးကွက်ဖွင့်ချိန် |
| `"New York"` | နယူးယောက်စျေးကွက်ဖွင့်ချိန် |
| `"Asian kill zone"` | ICT Asian Kill Zone |
| `"London open kill zone"` | ICT London Open Kill Zone |
| `"New York kill zone"` | ICT New York Kill Zone |
| `"London close kill zone"` | ICT London Close Kill Zone |
| `"Custom"` | ကိုယ်ပိုင်အချိန်သတ်မှတ်ရန် |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `Active` | Candle သည် session အတွင်းဖြစ်လျှင် 1၊ မဟုတ်လျှင် 0 |
| `High` | Session အတွင်း အမြင့်ဆုံးစျေးနှုန်း |
| `Low` | Session အတွင်း အနိမ့်ဆုံးစျေးနှုန်း |

> **အသုံးပြုပုံ** - ICT Kill Zone တွေအတွင်း အရောင်းအဝယ်ပြုလုပ်ခြင်း၊ Session High/Low Breakout နည်းဗျူဟာများအတွက် အလွန်အသုံးဝင်ပါတယ်။

### ၃.၃ Retracements - `smc.retracements()`

**သဘောတရား** - Swing High သို့မဟုတ် Swing Low မှ စျေးနှုန်း ပြန်လည်ဆုတ်ခွာသွားသည့် ရာခိုင်နှုန်းကို တွက်ချက်ပေးပါသည်။ Fibonacci retracement နှင့် ဆင်တူသော်လည်း အချိန်နှင့်တပြေးညီ retracement % ကို ပေးပါသည်။

| Parameter | အမျိုးအစား | ရှင်းလင်းချက် |
|-----------|------------|----------------|
| `ohlc` | DataFrame | OHLC ဒေတာ |
| `swing_highs_lows` | DataFrame | `swing_highs_lows()` function မှ ရရှိသော DataFrame |

| Return Column | ရှင်းလင်းချက် |
|---------------|----------------|
| `Direction` | 1 = Bullish retracement, -1 = Bearish retracement |
| `CurrentRetracement%` | Swing High/Low မှ လက်ရှိ retracement ရာခိုင်နှုန်း |
| `DeepestRetracement%` | Swing High/Low မှ အနက်ရှိုင်းဆုံး retracement ရာခိုင်နှုန်း |

> **အသုံးပြုပုံ** - Retracement ဘယ်လောက်ထိ ဆုတ်သွားလဲ သိရှိနိုင်ပြီး၊ Fibonacci 61.8%, 79% စသည့် level တွေနဲ့ တွဲဖက်အသုံးပြုနိုင်ပါတယ်။

---
## ၄။ Hide Credit Message

Library ကို import လုပ်တဲ့အခါ credit message ပြသခြင်းကို အောက်ပါ environment variable ဖြင့် ပိတ်ထားနိုင်ပါတယ်။

```bash
export SMC_CREDIT=0
```

---
## ၅။ PyPI Package vs GitHub Repository နှိုင်းယှဉ်ချက်

| အင်္ဂါရပ် | PyPI (`smartmoneyconcepts`) | GitHub (`joshyattridge/smart-money-concepts`) |
|-----------|----------------------------|-----------------------------------------------|
| FVG | ✓ | ✓ |
| Swing Highs/Lows | ✓ | ✓ |
| BOS/CHoCH | ✓ | ✓ |
| Order Blocks | ✓ | ✓ |
| Liquidity | ✓ | ✓ |
| Previous High/Low | ✗ | ✓ (ထပ်တိုး) |
| Sessions | ✗ | ✓ (ထပ်တိုး) |
| Retracements | ✗ | ✓ (ထပ်တိုး) |
| Hide Credit Message | ✗ | ✓ |
| Source Code | Compiled package | မူရင်း Python code |
| Contributing Guide | ✗ | ✓ |

GitHub repository က PyPI ထက် ပိုမိုပြည့်စုံပြီး နောက်ဆုံးထွက် feature တွေ ပါဝင်ပါတယ်။ PyPI မှာ ဖော်ပြထားတဲ့ README က အတိုချုံးဖြစ်ပြီး၊ GitHub README ကတော့ indicator ၈ မျိုးလုံးကို အပြည့်အစုံ ဖော်ပြထားပါတယ်။

---
## ၆။ Contributing (ပါဝင်ကူညီနိုင်ပုံ)

Repository မှာ open-source project ဖြစ်တဲ့အတွက် အောက်ပါအတိုင်း ပါဝင်ကူညီနိုင်ပါတယ်။

1. Repository ကို Fork လုပ်ပါ။
2. ကုဒ်တည်ဆောက်ပုံကို လေ့လာပါ။
3. Feature branch တစ်ခု ဖန်တီးပါ (`git checkout -b my-new-feature`)။
4. ပြင်ဆင်မှုများကို Commit လုပ်ပါ (`git commit -am 'Add some feature'`)။
5. Branch သို့ Push တင်ပါ (`git push origin my-new-feature`)။
6. Pull Request အသစ်တစ်ခု ဖန်တီးပါ။

> **မှတ်ချက်** - Pull Request တစ်ခုစီသည် function တစ်ခုတည်း သို့မဟုတ် feature အသေးစားတစ်ခုတည်းကိုသာ အာရုံစိုက်သင့်ပြီး၊ ကြီးမားကျယ်ပြန့်သော ပြောင်းလဲမှုများကို လက်ခံမည်မဟုတ်ပါ။

---
## ၇။ Repository များကြား ဆက်စပ်မှု

GitHub ပေါ်မှာ ဒီ project နဲ့ သက်ဆိုင်တဲ့ repository ၃ ခု ရှိပါတယ်။

| Repository | Stars | ရှင်းလင်းချက် |
|------------|-------|----------------|
| `joshyattridge/smart-money-concepts` | 138 | **မူရင်း repository** - Josh Attridge ကိုယ်တိုင် ထိန်းသိမ်းသည် |
| `leero-ady/smart-money-concepts` | 772 | PyPI နှင့် ချိတ်ဆက်ထားသော mirror - နာမည်အကြီးဆုံး |
| `jemmy655/smartmoneyconcepts-joshyattridge` | 2 | အဟောင်း fork တစ်ခု (2023) |

`joshyattridge` နှင့် `leero-ady` တို့သည် တစ်ဦးတည်းသော ပုဂ္ဂိုလ် (Josh Attridge) ၏ GitHub account နှစ်ခု ဖြစ်နိုင်ပြီး `leero-ady` က PyPI package publishing အတွက် အသုံးပြုတာ ဖြစ်ပါတယ်။

---
## ၈။ MT5 နှင့် ပေါင်းစပ်အသုံးပြုခြင်း

GitHub repository ကိတော့ PyPI package အတိုင်းပဲ MT5 နဲ့ တွဲသုံးနိုင်ပါတယ်။ ဒါပေမယ့် GitHub မှာပါတဲ့ indicator အသစ် ၃ ခုကိုပါ ထည့်သုံးချင်ရင် `pip install` လုပ်မယ့်အစား repository ကနေ တိုက်ရိုက် install လုပ်နိုင်ပါတယ်။

```bash
# GitHub ကနေ တိုက်ရိုက် install လုပ်ခြင်း
pip install git+https://github.com/joshyattridge/smart-money-concepts.git
```

ထို့နောက် Sessions indicator ကို MT5 data နဲ့ တွဲသုံးပုံ နမူနာ:

```python
import MetaTrader5 as mt5
import pandas as pd
from smartmoneyconcepts import smc

mt5.initialize()

# MT5 မှ M15 data ဆွဲထုတ်ပါ
rates = mt5.copy_rates_from_pos("EURUSD", mt5.TIMEFRAME_M15, 0, 1000)
df = pd.DataFrame(rates)
df.columns = ["time", "open", "high", "low", "close", "tick_volume", "spread", "real_volume"]
df = df[["open", "high", "low", "close", "tick_volume"]]
df.rename(columns={"tick_volume": "volume"}, inplace=True)

# London Kill Zone session စစ်ဆေးပါ
london_kz = smc.sessions(df, session="London open kill zone", time_zone="UTC+0")

# Session အတွင်းရှိ candle များကို filter လုပ်ပါ
session_candles = df[london_kz['Active'] == 1]

mt5.shutdown()
```

---
## ၉။ Disclaimer

Repository မှာ အောက်ပါ သတိပေးချက် ပါဝင်ပါတယ်။

> ဤ project သည် ပညာရေးဆိုင်ရာ ရည်ရွယ်ချက်အတွက်သာ ဖြစ်သည်။ ဤ indicator ကို ကုန်သွယ်မှုဆုံးဖြတ်ချက်များ၏ တစ်ခုတည်းသော အခြေခံအဖြစ် အသုံးမပြုပါနှင့်။ ကုန်သွယ်မှုမပြုလုပ်မီ သင့်လျော်သော စွန့်စားမှုစီမံခန့်ခွဲမှုကို အမြဲအသုံးပြုပြီး သင့်ကိုယ်ပိုင် သုတေသနပြုလုပ်ပါ။

---
## ၁၀။ အကျဉ်းချုပ်

`joshyattridge/smart-money-concepts` GitHub repository သည် `smartmoneyconcepts` PyPI package ၏ source code တည်ရှိရာဖြစ်ပြီး PyPI မှာ မပါဝင်သေးသော indicator ၃ ခု (Previous High/Low, Sessions, Retracements) ကို ထပ်တိုးပေးထားပါတယ်။ 138 stars နှင့် 83 forks ရှိပြီး ICT Smart Money Concepts ကို Python algorithmic trading အတွက် အကောင်အထည်ဖော်ထားတဲ့ open-source project တစ်ခုဖြစ်ပါတယ်။ PyPI package ကို `pip install smartmoneyconcepts` နဲ့ install လုပ်နိုင်သလို၊ နောက်ဆုံးထွက် feature တွေကို လိုချင်ရင် GitHub ကနေ တိုက်ရိုက် clone လုပ်ပြီးလည်း သုံးနိုင်ပါတယ်။


