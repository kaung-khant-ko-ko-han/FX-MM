# 📡 Telegram to MT4 / MT5 Signal Trader - အသေးစိတ် ရှင်းလင်းချက်

ဒီ Blog post ဟာ **Telegram ကနေ တိုက်ရိုက် MetaTrader (MT4/MT5) ကို Signal တွေ ကူးယူပေးတဲ့** ဆော့ဖ်ဝဲတစ်ခုအကြောင်း ဖြစ်ပါတယ်။ ဖန်တီးသူက **Lukas Roth** (MQL5 အကောင့်အမည်) ဖြစ်ပြီး MQL5 Marketplace မှာ ရောင်းချထားတဲ့ ထုတ်ကုန်တစ်ခုပါ။

---

## ၁။ ဒီ Software က ဘာလုပ်ပေးလဲ။

| လုပ်ဆောင်ချက် | ရှင်းလင်းချက် |
|---------------|----------------|
| Telegram မှ Signal ကူးခြင်း | Telegram အဖွဲ့များ / ချန်နယ်များမှ စာသားအခြေပြု ကုန်သွယ်ရေး Signal များကို MT4/MT5 သို့ **အလိုအလျောက်** ကူးယူပေးသည် |
| Public & Private | အများသုံး ချန်နယ်များနှင့် Private အဖွဲ့/ချန်နယ် နှစ်မျိုးလုံးကို ထောက်ပံ့ |
| Provider အများအပြား | Signal ပေးသူ **၁၀ ဦးအထိ** တစ်ပြိုင်နက် ချိတ်ဆက်နိုင်သည် |
| အကောင့်အများအပြား | Signal များကို MT4/MT5 အကောင့် တစ်ခု သို့မဟုတ် တစ်ခုထက်ပို၍ တစ်ပြိုင်နက် ပို့ဆောင်နိုင်သည် |

---

## ၂။ Install လုပ်နည်း (အဆင့်ဆင့်)

ဒီဆော့ဖ်ဝဲဟာ **Windows မှာသာ အလုပ်လုပ်ပါတယ်**။ Linux သို့မဟုတ် macOS အတွက် မရသေးပါ။

### အဆင့် ၁ - EA ကို MQL5 Marketplace မှ ဝယ်ယူ/Install လုပ်ပါ
- `Telegram to MT5 Signal Trader` EA ကို MQL5 Marketplace မှ install လုပ်ပါ

### အဆင့် ၂ - Web Request ခွင့်ပြုပါ
- MetaTrader Terminal → Tools → Options → Expert Advisors → **"Allow WebRequest for listed URL"** ကို အမှန်ခြစ်ပြီး `http://127.0.0.1:5000` ကို ထည့်ပါ

### အဆင့် ၃ - Desktop Application ကို Download လုပ်ပါ
- GitHub မှ `Signal Trader` desktop software ကို download လုပ်ပြီး install လုပ်ပါ (`Telegram.Signal.Trader_0.4.0_x64_en-US.msi` စသည့် ဖိုင်အမည်ဖြင့်)

### အဆင့် ၄ - Login လုပ်ပါ
1. Signal Trader App ကိုဖွင့်
2. EA ကို MetaTrader မှာ run ထားကြောင်း သေချာပါစေ (မရှိရင် Login မရပါ)
3. ဖုန်းနံပါတ် (Country Code ပါ) ထည့်ပါ
4. Telegram မှ ရောက်လာတဲ့ Code ထည့်ပါ
5. 2FA Password ရှိရင် ထည့်ပါ

---

## ၃။ Navigation Menu (ဘေးဘားလမ်းညွှန်)

Desktop Application ရဲ့ ဘယ်ဘက်ခြမ်းမှာ အောက်ပါ Menu များ ပါဝင်ပါတယ်。

| Menu | လုပ်ဆောင်ချက် |
|------|---------------|
| **Home** | ဗားရှင်းအသစ်မှတ်တမ်းနှင့် Demo Video |
| **Account** | အကောင့်များ၊ Provider များ၊ Orders များ၊ Signals များ |
| **Products** | ဆက်စပ် ထုတ်ကုန်များ လင့်ခ် |
| **Help** | လက်စွဲနှင့် Demo Video |
| **Support** | Bug Report / Feature Request တင်ရန် |
| **Logs** | Application Log ဖိုင်ကြည့်ရှုရန် |
| **Settings** | App Update စစ်ဆေးရန် |

---

## ၄။ Account & Provider များ သတ်မှတ်ခြင်း

### Account ဖန်တီးခြင်း
Sidebar မှ **Account** ကိုနှိပ်ပါ။ အနည်းဆုံး Signal Account တစ်ခု ဖန်တီးရန် လိုအပ်ပါသည်။ Account တစ်ခုစီဟာ MetaTrader မှာ run နေတဲ့ EA instance တစ်ခုနဲ့ ချိတ်ဆက်ပါတယ်။

### Provider ဆိုတာ ဘာလဲ။
**Provider** ဆိုတာ Telegram ပေါ်က Signal ပေးသူ ချန်နယ်/အဖွဲ့ ကို ဆိုလိုပါတယ်။

| လုပ်ဆောင်နိုင်စွမ်း | အသေးစိတ် |
|---------------------|------------|
| Provider ထည့်သွင်းခြင်း | "Add Provider" ကတ်ကိုနှိပ်ပြီး မိမိ၏ Telegram ချက်များစာရင်းမှ ရွေးချယ်နိုင် |
| Provider အရေအတွက် | Account တစ်ခုလျှင် **၁၀ ဦးအထိ** ထည့်သွင်းနိုင် |
| Provider Settings | Provider အတွက် သီးသန့် ချိန်ညှိချက်များ |

---

## ၅။ Orders & Signals ဇယားများ

| ဇယား | ကြည့်ရှုနိုင်သည်များ |
|------|---------------------|
| **Orders** | Provider အလိုက်၊ Status (Open/Closed/Pending/Cancelled) အလိုက် Filter လုပ်နိုင်သည် |
| **Signals** | Telegram မှ ဖတ်ယူထားသော Signal အားလုံးကို Provider/Status အလိုက် စစ်ကြည့်နိုင်သည် |

---

## ၆။ Account Settings (အကောင့်အဆင့် ချိန်ညှိချက်များ)

အောက်ပါ Setting များသည် **Signal အကောင့်တစ်ခုလုံး** အတွက် အကျုံးဝင်ပြီး၊ **Signal Provider များမှ ဖွင့်သော အရောင်းအဝယ်များ** အတွက်သာ သက်ရောက်ပါသည်။ Manual အရောင်းအဝယ် သို့မဟုတ် အခြား EA များမှ အရောင်းအဝယ်များကို **ထည့်သွင်းစဉ်းစားမည်မဟုတ်ပါ**။

### ၆.၁ Symbol ဆက်စပ် ချိန်ညှိချက်များ

| Setting | ရှင်းလင်းချက် |
|---------|---------------|
| **Symbol Prefix/Suffix** | Broker က x.EURUSD, EURUSD.i စသည်ဖြင့် သုံးထားလျှင် သတ်မှတ်ပေးရန်လို |
| **Exclude/Include Symbols** | အချို့ Symbol များကို တားမြစ်ရန် (သို့) ခွင့်ပြုရန် |
| **Custom Symbol Mappings** | Provider က "Buy Gold" လို့ ရေးလျှင် `Gold → XAUUSD` ဟု မြေပုံချိတ်ဆက်ပေးခြင်း |

### ၆.၂ စွန့်စားမှု စီမံခန့်ခွဲမှု (Risk Settings)

| Risk Type | ရှင်းလင်းချက် |
|-----------|---------------|
| **Fixed Money** | ပုံသေငွေပမာဏဖြင့် |
| **% of Balance** | အကောင့်လက်ကျန်၏ ရာခိုင်နှုန်း |
| **% of Equity** | Equity (Balance + Floating PnL) ၏ ရာခိုင်နှုန်း |
| **Fixed Lot Size** | ပုံသေ Lot Size |

### ၆.၃ Profit & Loss Protection (အကာအကွယ်)

နေ့စဉ်/အပတ်စဉ်/လစဉ် အမြတ် သို့မဟုတ် အရှုံး ကန့်သတ်ချက် ရောက်သည်နှင့် **အရောင်းအဝယ်အားလုံး ပိတ်ပြီး ကျန်ကာလအတွက် အရောင်းအဝယ်အသစ် လုံးဝမလုပ်တော့ပါ**။

> ⚠️ **Prop Firm သတိပေးချက်:** Prop Firm အကောင့်များအတွက် စည်းမျဉ်းကန့်သတ်ချက်ထက် **နိမ့်သော ကန့်သတ်ချက်** သတ်မှတ်သင့်သည်။

### ၆.၄ အရောင်းအဝယ် ကန့်သတ်ချက်များ

| Setting | ရှင်းလင်းချက် |
|---------|---------------|
| **Max Open Trades** | တစ်ပြိုင်နက် ဖွင့်နိုင်သည့် အများဆုံး အရောင်းအဝယ် |
| **Max Trades Per Minute/Hour/Day/Week/Month** | အချိန်ကာလအလိုက် အများဆုံး ဖွင့်နိုင်သည့် အရောင်းအဝယ် |
| **Max Trades Per [Custom Period]** | စိတ်ကြိုက်အချိန်ကာလ (ဥပမာ ၃ ရက်တစ်ကြိမ်) သတ်မှတ်နိုင် |

### ၆.၅ ကုန်သွယ်မှုအချိန် ချိန်ညှိချက်များ

| Setting | ရှင်းလင်းချက် |
|---------|---------------|
| **Allowed Trading Days** | ကုန်သွယ်ခွင့်ပြုသည့် ရက်များ |
| **Trading Time Restrictions** | ကုန်သွယ်မှုပိတ်မည့် အချိန်များ (ဥပမာ တနင်္လာ ၂၂:၀၀ မှ အင်္ဂါ ၀၆:၀၀) |
| **Auto Close Settings** | အပတ်စဉ် သတ်မှတ်ရက်နှင့် အချိန်တွင် အားလုံးအလိုအလျောက်ပိတ်ရန် |

### ၆.၆ သတင်းစစ်ထုတ်မှု (News Filtering)

| News Impact | ရှင်းလင်းချက် |
|-------------|---------------|
| **Low Impact** | သတင်းမထွက်မီနှင့် ထွက်ပြီးနောက် သတ်မှတ်ထားသော မိနစ်အတွင်း Signal များကို တားမြစ် |
| **Medium Impact** | ထိုနည်းတူ သတ်မှတ်နိုင် |
| **High Impact** | မဖြစ်မနေ တားမြစ်သင့် (စျေးကွက်မတည်ငြိမ်မှုအတွက်) |
| **Consider News Affecting Currency** | Symbol နှင့် သက်ဆိုင်သော သတင်းများကိုသာ စစ်ထုတ်ရန် |

### ၆.၇ အကြောင်းကြားချက်များ (Notifications)

| နည်းလမ်း | ရှင်းလင်းချက် |
|-----------|---------------|
| **Email** | MT Terminal → Tools → Options → Email တွင် သတ်မှတ်ရန် |
| **Mobile App** | MQL5 ID ဖြင့် Push Notification |
| **Telegram** | Bot Token ဖြင့် ချိတ်ဆက်ကာ အကြောင်းကြား |

အကြောင်းကြားမည့် အဖြစ်အပျက်များ: Trade Open, Trade Close, Order Cancel, Order Modify

---

## ၇။ Provider Settings (Provider အဆင့် ချိန်ညှိချက်များ)

Provider Settings သည် **Provider တစ်ဦးချင်းစီအတွက် သီးသန့်** ချိန်ညှိနိုင်သည်။ ဤသည်မှာ အလွန်အရေးကြီးသော Setup အပိုင်းဖြစ်သည်။

### ၇.၁ အခြေခံများ

| Setting | ရှင်းလင်းချက် |
|---------|---------------|
| **Default Symbol** | Signal တွင် Symbol မပါလျှင် သုံးမည့် Symbol |
| **Trade Action Filters** | Market Orders, Pending Orders, Partial Closes, Breakeven Events, Order Modifications, Deletions, Reopenings တစ်ခုချင်းစီကို ဖွင့်/ပိတ်နိုင် |
| **Signal Behavior** | မူရင်း Telegram စာတို ပြင်ဆင်ခြင်း/ဖျက်ပစ်ခြင်း ခံရလျှင် အရောင်းအဝယ်ကို Update လုပ်မလား၊ Close လုပ်မလား |
| **Ignore Incomplete Signals** | SL, TP စသည့် အချက်အလက်မပြည့်စုံသော Signal များကို ကျော်သွားရန် |

### ၇.၂ Value Detection (တန်ဖိုး ဖော်ထုတ်ခြင်း)

ကွဲပြားသော ဒေသသုံး နံပါတ်ပုံစံများ (ဒဿမနှင့် ထောင်ဂဏန်းခွဲခြားပုံ) ကို သတ်မှတ်နိုင်သည်။

### ၇.၃ Order Types (အမှာစာ အမျိုးအစားများ)

| Order Type | သတ်မှတ်နိုင်သော သော့ချက်စာလုံးများ |
|------------|-----------------------------------|
| **Buy** | `buy`, `long`, `bullish` |
| **Sell** | `sell`, `short`, `bearish` |

### ၇.၄ Signal Actions (Signal လုပ်ဆောင်ချက်များ)

Signal စာတိုကို Pattern ဖြင့် ဖော်ထုတ်ဖတ်ယူသည်။ ဥပမာအားဖြင့်:

**Signal:** `Gold buy now 3369.3 - 3366 SL: 3363 TP: 3371 TP: 3373 TP: 3375`

ဤ Signal ကို နားလည်နိုင်ရန် Provider Settings တွင် Pattern သတ်မှတ်ပေးရပါမည်။ အောက်ပါ Tag များ သုံးနိုင်သည်-
- `{SYMBOL}` - Symbol ကို ကိုယ်စားပြု
- `{TYPE}` - Order Type ကို ကိုယ်စားပြု
- `{PRICE}` - စျေးနှုန်း ကို ကိုယ်စားပြု

### ၇.၅ Trade Levels (SL/TP/BE သတ်မှတ်ခြင်း)

SL, TP, Entry, Break-even စသည့် Level များအတွက်-
1. သော့ချက်စာလုံး (ဥပမာ `SL`, `Stop loss`, `sl` အားလုံးကို SL အဖြစ် အသိအမှတ်ပြုရန်)
2. Format Pattern (ဥပမာ `SL: 3363` → pattern က `: {VALUE}`)

### ၇.၆ Risk Settings (Provider အဆင့်)

Provider တစ်ဦးချင်းစီအတွက် စွန့်စားမှု သတ်မှတ်နိုင်သည်။

| Setting | ရှင်းလင်းချက် |
|---------|---------------|
| Stop Loss | Manual SL သတ်မှတ်ခြင်း၊ Signal တွင် SL မပါမှသာ Manual SL ကိုသုံးရန် ရွေးချယ်နိုင် |
| **Break-Even** | Pip အတိုင်းအတာတစ်ခု အမြတ်ရပြီးနောက် SL ကို Breakeven သို့ ရွှေ့ရန် |
| **Trailing Stop** | အမြတ် သတ်မှတ်ချက်ရောက်ပါက နောက်ကလိုက်သည့် SL စတင်ရန် |
| **Partial Close** | TP Level တစ်ခုစီတွင် Position ၏ မည်မျှရာခိုင်နှုန်း ပိတ်မည်ကို သတ်မှတ် |
| **TP Strategy** | TP2 ထိသွားလျှင် SL ကို Entry သို့ (သို့) TP1 သို့ ရွှေ့ရန် စသည့် နည်းဗျူဟာ |

### ၇.၇ Entry Price နှင့် Slippage

| Setting | ရှင်းလင်းချက် |
|---------|---------------|
| **Slippage Handling** | Entry Price ကို လျစ်လျူရှုမလား၊ Slippage ကျော်လျှင် Pending Order အဖြစ် ပြောင်းမလား |
| **Max Allowed Slippage** | ခွင့်ပြုနိုင်သော Slippage အများဆုံးပမာဏ |
| **Pending Order Expiry** | Pending Order သက်တမ်းကုန်ချိန် (မိနစ်ဖြင့်) |
| **Entry Offset** | Prop Firm များအတွက် Signal Entry မှ အနည်းငယ်ကွာချင်လျှင် Offset သတ်မှတ်နိုင် |
| **Entry Range Mode** | Best, Worst, Average, Market Adaptive စသည်ဖြင့် ရွေးချယ်နိုင် |

### ၇.၈ Tick Value ပြင်ဆင်ခြင်း

CFD Broker အချို့တွင် Tick Value မှားယွင်းနေတတ်ပြီး Risk တွက်ချက်မှု မှားသွားနိုင်ပါသည်။ ထိုအခါ-
- `XAUUSD=10` ကဲ့သို့ အချိုးထည့်ပေးခြင်း
- `Adjust tick value to account currency` ဖြင့် Broker ၏ Tick Value ပြဿနာကို ကိုယ်တိုင်ပြင်ဆင်ခြင်း

---

## ၈။ အသုံးဝင်သော အကာအကွယ်များ အကျဉ်းချုပ်

| အကာအကွယ် | ရှင်းလင်းချက် |
|-------------|---------------|
| **Profit/Loss Protection** | နေ့/အပတ်/လ အလိုက် အမြတ်/အရှုံး ကန့်သတ်ချက် |
| **Max Open Trades** | တစ်ပြိုင်နက် အရောင်းအဝယ် အရေအတွက် ကန့်သတ် |
| **Trade Frequency** | တစ်မိနစ်/နာရီ/ရက်/အပတ်/လ အလိုက် အကြိမ်ရေ ကန့်သတ် |
| **Trading Days & Hours** | သတ်မှတ်ရက်နှင့် အချိန်များတွင် ကုန်သွယ်မှုပိတ် |
| **News Filter** | စီးပွားရေးသတင်းများအတွင်း အရောင်းအဝယ် တားမြစ် |
| **Equity Protection** | Equity ကျဆင်းမှုအတိုင်းအတာ ရောက်လျှင် အရောင်းအဝယ်ရပ်ရန် |

---

## ၉။ ကန့်သတ်ချက်များ

| ကန့်သတ်ချက် | ရှင်းလင်းချက် |
|---------------|----------------|
| **Windows Only** | Linux/macOS မရသေး (Windows VPS သုံးရန် အကြံပြု) |
| **Demo Version** | Demo Version မရှိသေး (တိုက်ရိုက်ဝယ်ယူရန်) |
| **Desktop App လိုအပ်** | MQL ကန့်သတ်ချက်ကြောင့် EA အပြင် Desktop App လည်း လိုအပ် |
| **စာသား Signal သာ** | Telegram ပေါ်က စာသားအခြေပြု Signal ကိုသာ ဖတ်နိုင်သည် |

---

## ၁၀။ အကျဉ်းချုပ်

ဤ Blog Post သည် **"Telegram to MT4/MT5 Signal Trader"** ဆိုသည့် MQL5 Marketplace ထုတ်ကုန်တစ်ခု၏ **ပြည့်စုံသော လက်စွဲတစ်ပိုင်းတစ်စ** ဖြစ်ပါသည်။

| အချက် | ဖော်ပြချက် |
|--------|------------|
| **ရေးသားသူ** | Lukas Roth |
| **ရည်ရွယ်ချက်** | Telegram Signal များကို MT4/MT5 သို့ အလိုအလျောက် ကူးယူရန် |
| **Platform** | Windows Only (VPS အကြံပြု) |
| **လိုအပ်ချက်** | EA + Desktop Application နှစ်ခုလုံး Install လုပ်ရန် |
| **ထူးခြားချက်** | Risk Management, News Filter, Equity Protection စသည့် Professional Features များစွာ ပါဝင် |
| **Price** | MQL5 Marketplace တွင် အခကြေးငွေဖြင့် ဝယ်ယူရသည် |

Signal စာတိုများကို Pattern ဖြင့် ဖော်ထုတ်ဖတ်ယူနိုင်သောကြောင့် **မည်သည့် Telegram Signal Provider နှင့်မဆို တွဲဖက်အသုံးပြုနိုင်ပါသည်**။ Demo Account ဖြင့် ဦးစွာ စမ်းသပ်ရန် အကြံပြုထားသည်။

---

Github Link : https://github.com/LukiRoth/Signal-Trader-Release

Github Link : https://github.com/LukiRoth/Signal-Trader-Release/releases/tag/v0.8.10-beta

🔗 Download: https://mql5.com/8co9h

📖 User Guide: https://www.mql5.com/en/blogs/post/763228

Socials
📌 MetaQuotes profile: https://mql5.com/en/users/lukiroth

🚀 Join my Telegram Channel: https://t.me/BestTradingEAs

Youtube: https://youtu.be/FxZ0dQ8CZbQ



