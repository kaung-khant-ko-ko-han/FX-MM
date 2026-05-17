ဤအကြောင်းအရာသည် AnyChart စာကြည့်တိုက် (Library) ကို အသုံးပြု၍ OHLC ဇယားများ ဖန်တီးခြင်းဆိုင်ရာ နည်းပညာဆိုင်ရာ စာရွက်စာတမ်းဖြစ်ပါသည်။ သင်ရှာဖွေနေသော အချက်အလက်များကို အောက်ပါအတိုင်း မြန်မာဘာသာဖြင့် ပြန်ဆိုထားပါသည်။

---

## AnyChart တွင် OHLC ဇယားများ ဖန်တီးခြင်း လမ်းညွှန်

### ၁။ OHLC ဇယားဆိုသည်မှာ

Open-High-Low-Close (OHLC) ဇယားသည် အချိန်နှင့်အမျှ ငွေကြေးဆိုင်ရာ ပစ္စည်းတစ်ခု၏ ဈေးနှုန်းလှုပ်ရှားမှုများကို သရုပ်ဖော်ရန် အဓိကအသုံးပြုသော ဇယားအမျိုးအစားတစ်ခုဖြစ်သည်။ ဒေါင်လိုက်မျဉ်းတစ်ကြောင်းချင်းစီသည် အချိန်ကာလတစ်ခုအတွင်း ဈေးနှုန်းအကွာအဝေး (အမြင့်ဆုံးနှင့် အနိမ့်ဆုံးဈေးနှုန်းများ) ကို ပြသပြီး ဘယ်ဘက်ရှိ အလျားလိုက်အမှတ်အသားက အဖွင့်ဈေးနှုန်း၊ ညာဘက်ရှိ အမှတ်အသားက အပိတ်ဈေးနှုန်းတို့ကို ကိုယ်စားပြုပါသည်။

OHLC ဇယားနှင့် Japanese Candlestick ဇယားတို့သည် တူညီသော အချက်အလက်များ (အဖွင့်၊ အမြင့်၊ အနိမ့်၊ အပိတ်) ကို ဖော်ပြသော်လည်း ဖော်ပြပုံချင်း ကွဲပြားပါသည်။ အချို့ကုန်သည်များက Japanese Candlestick ဇယားကို ဖတ်ရှုရန် ပိုမိုလွယ်ကူသည်ဟု ယူဆကြသည်။

### ၂။ OHLC ဇယား၏ အခြေခံအစိတ်အပိုင်းများ

OHLC ဇယားတစ်ခုတွင် အောက်ပါအချက်အလက် လေးချက် ပါဝင်ပါသည်။

| အတိုကောက် | အဓိပ္ပါယ် | ဖော်ပြချက် |
|:---|:---|:---|
| **O** | Open (အဖွင့်) | သတ်မှတ်ထားသော အချိန်ကာလ၏ ပထမဆုံးဈေးနှုန်း (ဘယ်ဘက်အမှတ်အသား) |
| **H** | High (အမြင့်) | သတ်မှတ်ထားသော အချိန်ကာလအတွင်း အမြင့်ဆုံးဈေးနှုန်း (ဒေါင်လိုက်မျဉ်းထိပ်) |
| **L** | Low (အနိမ့်) | သတ်မှတ်ထားသော အချိန်ကာလအတွင်း အနိမ့်ဆုံးဈေးနှုန်း (ဒေါင်လိုက်မျဉ်းအောက်ခြေ) |
| **C** | Close (အပိတ်) | သတ်မှတ်ထားသော အချိန်ကာလ၏ နောက်ဆုံးဈေးနှုန်း (ညာဘက်အမှတ်အသား) |

ဈေးနှုန်းများ မြင့်တက်သည်ဖြစ်စေ၊ ကျဆင်းသည်ဖြစ်စေ ပေါ်မူတည်၍ ဘားများကို မတူညီသော အရောင်များဖြင့် ဖော်ပြနိုင်သည်။

### ၃။ AnyChart တွင် OHLC ဇယားတစ်ခု စတင်ဖန်တီးခြင်း (Quick Start)

AnyChart တွင် OHLC ဇယားတစ်ခုကို ဖန်တီးရန် အောက်ပါအဆင့်များကို လုပ်ဆောင်ရပါမည်။

#### အဆင့် (၁) - HTML စာမျက်နှာ ဖန်တီးခြင်း

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>JavaScript OHLC Chart</title>
    <style type="text/css">
        html, body, #container {
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
        }
    </style>
</head>
<body>
    <div id="container"></div>
</body>
</html>
```

#### အဆင့် (၂) - လိုအပ်သော JavaScript Modules များထည့်သွင်းခြင်း

AnyChart OHLC ဇယားအတွက် Core နှင့် Basic Cartesian modules များ (သို့မဟုတ် Base module) လိုအပ်ပါသည်။ CDN မှတစ်ဆင့် ထည့်သွင်းနိုင်သည်-

```html
<script src="https://cdn.anychart.com/releases/8.11.1/js/anychart-core.min.js"></script>
<script src="https://cdn.anychart.com/releases/8.11.1/js/anychart-stock.min.js"></script>
<script src="https://cdn.anychart.com/releases/8.11.1/js/anychart-data-adapter.min.js"></script>
```

#### အဆင့် (၃) - ဒေတာဖွဲ့စည်းပုံ

OHLC ဇယားအတွက် ဒေတာကို Array of Arrays သို့မဟုတ် Array of Objects ပုံစံဖြင့် ထည့်သွင်းနိုင်သည်။ ဒေတာတွင် `x`, `open`, `high`, `low`, `close` ဟူသော Data Fields များ ပါဝင်ရပါမည်။ အောက်ပါအတိုင်း ဒေတာကို mapping လုပ်နိုင်သည်-

```javascript
var mapping = dataTable.mapAs({
    date: 0,
    open: 1,
    high: 2,
    low: 3,
    close: 4
});
```

#### အဆင့် (၄) - OHLC ဇယားကုဒ် ရေးသားခြင်း

OHLC ဇယားကို ဖန်တီးရန် `anychart.ohlc()` chart constructor ကိုအသုံးပြုပြီး `ohlc()` method ဖြင့် OHLC series ကို ဖန်တီးပါသည်။

```javascript
// ဒေတာ ဖန်တီးခြင်း
var data = [
    [Date.UTC(2007, 07, 23), 23.55, 23.88, 23.38, 23.62],
    [Date.UTC(2007, 07, 24), 22.65, 23.70, 22.65, 23.36],
    [Date.UTC(2007, 07, 25), 22.75, 23.70, 22.69, 23.44],
];

// ဇယားဖန်တီးခြင်း
chart = anychart.ohlc();

// OHLC series ဖန်တီးပြီး ဒေတာထည့်သွင်းခြင်း
var series = chart.ohlc(data);

// ဇယားအတွက် container သတ်မှတ်ခြင်း
chart.container("container");

// ဇယားဆွဲခြင်း
chart.draw();
```

### ၄။ OHLC ဇယား၏ အသွင်အပြင် စိတ်ကြိုက်ပြင်ဆင်ခြင်း (Appearance Customization)

AnyChart တွင် OHLC series ၏ အသွင်အပြင်ကို အခြေအနေသုံးမျိုးဖြင့် ပြင်ဆင်သတ်မှတ်နိုင်သည်။

| အခြေအနေ | Method | ဖော်ပြချက် |
|:---|:---|:---|
| **Normal** | `normal()` | ပုံမှန်အခြေအနေ |
| **Hovered** | `hovered()` | မောက်စ်တင်ထားသည့်အခြေအနေ |
| **Selected** | `selected()` | ရွေးချယ်ထားသည့်အခြေအနေ |

#### Rising နှင့် Falling အရောင်များ သတ်မှတ်ခြင်း

ဈေးတက်သည့် (Rising) နှင့် ဈေးကျသည့် (Falling) ဘားများအတွက် သီးခြားအရောင်များ သတ်မှတ်နိုင်သည်။

```javascript
// ဈေးတက်သည့်အခြေအနေအတွက် အရောင်သတ်မှတ်ခြင်း
series1.normal().risingStroke("#33ccff");
series1.hovered().risingStroke("#33ccff", 1.5);
series1.selected().risingStroke("#33ccff", 3);

// ဈေးကျသည့်အခြေအနေအတွက် အရောင်သတ်မှတ်ခြင်း
series1.normal().fallingStroke("#ff33cc");
series1.hovered().fallingStroke("#ff33cc", 1.5);
series1.selected().fallingStroke("#ff33cc", 3);
```

#### နောက်ခံအရောင်နှင့် ဇယားအရောင်များ ပြင်ဆင်ခြင်း

```javascript
// ဇယားနောက်ခံအရောင်
chart.background().fill("#edf4f5");

// OHLC ဘားများ၏ အရောင်
ohlcSeries.fallingFill("#ff0d0d");
ohlcSeries.fallingStroke("#ff0d0d");
ohlcSeries.risingFill("#43ff43");
ohlcSeries.risingStroke("#43ff43");
```

#### Point Size နှင့် Labels များ

OHLC ဇယားတွင် Point Size များကို စိတ်ကြိုက်ပြင်ဆင်နိုင်ပြီး Labels (စာတမ်းများ) ကို ဇယားပေါ်ရှိ မည်သည့်နေရာတွင်မဆို ထည့်သွင်းနိုင်ကာ Font Settings နှင့် Text Formatters များကို အသုံးပြုနိုင်ပါသည်။

#### Tooltips များ

Tooltip ဆိုသည်မှာ ဇယားပေါ်ရှိ အမှတ်တစ်ခုပေါ်သို့ မောက်စ်တင်သည့်အခါ ပြသသည့် စာသားအကွက်ဖြစ်သည်။ Font Settings နှင့် Text Formatters များဖြင့် စာသားကို တည်းဖြတ်နိုင်ပြီး နောက်ခံပုံစံ၊ အနေအထား စသည်တို့ကို ပြောင်းလဲနိုင်ပါသည်။

### ၅။ အပိုဆောင်း အင်္ဂါရပ်များ (Additional Features)

#### Date Range Selection UI

ဇယားအောက်ခြေရှိ scroller အပြင် Date Range Picker နှင့် Range Selector တို့ကို ထည့်သွင်းနိုင်သည်။

```javascript
// ရက်စွဲအကွာအဝေး ရွေးချယ်မှုများ
var rangePicker = anychart.ui.rangePicker();
rangePicker.render(chart);

var rangeSelector = anychart.ui.rangeSelector();
rangeSelector.render(chart);
```

#### Event Markers များ

စတော့ဈေးကွက်အပေါ် သက်ရောက်မှုရှိသော ကမ္ဘာ့ဖြစ်ရပ်များကို ဇယားပေါ်တွင် အမှတ်အသားများအဖြစ် ထည့်သွင်းနိုင်သည်။

```javascript
plot.eventMarkers({
    "groups": [{
        "data": [{
            "symbol": "1",
            "date": "2020-03-11",
            "description": "WHO က COVID-19 ကို ကမ္ဘာ့ကပ်ရောဂါအဖြစ် ကြေညာခြင်း",
            "normal": {
                "type": "rect",
                "width": 40,
                "fill": "#ead9d1",
                "stroke": "2 #990033",
                "fontColor": "#990033",
                "fontWeight": 600,
                "connector": { "stroke": "2 #990033" }
            }
        }]
    }]
});
```

#### Vertical OHLC ဇယား

AnyChart တွင် Vertical OHLC ဇယားကိုလည်း ဖန်တီးနိုင်ပြီး `anychart.vertical()` chart constructor ကိုအသုံးပြုကာ `ohlc()` method ဖြင့် OHLC series ကို ဖန်တီးနိုင်သည်။

### ၆။ AnyChart OHLC ဇယား၏ နည်းပညာဆိုင်ရာ အချက်အလက်များ

| အမျိုးအစား | အသေးစိတ် |
|:---|:---|
| **Modules** | Core + Basic Cartesian (သို့မဟုတ် Base) |
| **API Class** | `anychart.core.cartesian.series.OHLC` |
| **Data Fields** | `x`, `open`, `high`, `low`, `close` |
| **Multiple Series** | ဟုတ်ကဲ့ (ထောက်ပံ့သည်) |
| **Stacked** | N/A |
| **Vertical** | ထောက်ပံ့သည် |
| **3D** | N/A |
| **Error Bars** | N/A |

### ၇။ နိဂုံးချုပ်

AnyChart စာကြည့်တိုက်သည် OHLC ဇယားများကို အလွယ်တကူ ဖန်တီးနိုင်ရန် အစွမ်းထက်သော API များကို ပေးဆောင်ထားပါသည်။ အခြေခံဇယားဖန်တီးမှုမှသည် အသွင်အပြင် စိတ်ကြိုက်ပြင်ဆင်မှုများ၊ Tooltips၊ Labels၊ Event Markers နှင့် Date Range Selectors များအထိ အဆင့်မြင့်အင်္ဂါရပ်များစွာကို အသုံးပြုနိုင်ပါသည်။ OHLC ဇယားများသည် စတော့ဈေးကွက်ဒေတာများကို သရုပ်ဖော်ရာတွင် အဓိကအသုံးပြုလေ့ရှိပြီး AnyStock တွင်လည်း အလားတူအသုံးပြုနိုင်ပါသည်။