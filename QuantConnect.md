```markdown
# LEAN ENGINE
## အပြည့်အဝ open-source algorithmic trading engine

စွယ်စုံပိုင်ဆိုင်မှုနှင့် portfolio modeling အပြည့်ဖြင့်၊ LEAN သည် data agnostic ဖြစ်ပြီး သင်ယခင်ကထက် ပိုမိုမြန်ဆန်စွာ စူးစမ်းနိုင်အောင် စွမ်းဆောင်ပေးသည်။

---

## Contents
1. Getting Started
2. Contributions
   2.1 Datasets
       2.1.1 Key Concepts
       2.1.2 Defining Data Models
       2.1.3 Rendering Data
           2.1.3.1 Rendering Data with Python
           2.1.3.2 Rendering Data with CSharp
           2.1.3.3 Rendering Data with Notebooks
       2.1.4 Testing Data Models
       2.1.5 Data Documentation
   2.2 Brokerages
       2.2.1 Setting Up Your Environment
       2.2.2 Laying the Foundation
       2.2.3 Creating the Brokerage
       2.2.4 Translating Symbol Conventions
       2.2.5 Describing Brokerage Limitations
       2.2.6 Enabling Live Data Streaming
       2.2.7 Enabling Historical Data
       2.2.8 Downloading Data
       2.2.9 Modeling Fee Structures
       2.2.10 Updating the Algorithm API
   2.3 Indicators
3. Data Format
   3.1 Key Concepts
   3.2 Core Data Types
4. Statistics
   4.1 Capacity
5. Class Reference

---

## Getting Started

### Introduction
Lean Engine သည် လွယ်ကူသော strategy သုတေသန၊ backtesting နှင့် live trading အတွက် တည်ဆောက်ထားသည့် open-source algorithmic trading engine တစ်ခုဖြစ်သည်။ ကျွန်ုပ်တို့သည် အသုံးများသော data providers နှင့် brokerages များနှင့် ပေါင်းစပ်ထားသောကြောင့် algorithmic trading strategies များကို လျင်မြန်စွာ deploy လုပ်နိုင်သည်။

LEAN Engine ၏ core ကို C# ဖြင့် ရေးသားထားသော်လည်း Linux, Mac နှင့် Windows operating systems များတွင် အဆင်ပြေစွာ အလုပ်လုပ်သည်။ ၎င်းသည် Python 3.11 သို့မဟုတ် C# ဖြင့် ရေးသားထားသော algorithms များကို support လုပ်သည်။ Lean သည် web-based algorithmic trading platform ဖြစ်သည့် QuantConnect ကို drive လုပ်ပေးသည်။

### System Overview
Engine ကို အခြားဖိုင်များကို မထိခိုက်ဘဲ extend လုပ်နိုင်သော modular အပိုင်းများစွာအဖြစ် ခွဲထားသည်။ Modules များကို config.json တွင် "environments" set အဖြစ် configure လုပ်ထားသည်။ ထို environments များမှတစ်ဆင့် LEAN ကို လိုအပ်သော mode အလိုက် ထိန်းချုပ်နိုင်သည်။

အရေးအကြီးဆုံး plugins များမှာ:

**Result Processing**  
Algorithmic trading engine မှ messages အားလုံးကို ကိုင်တွယ်သည့် ResultHandler။ မည်သည့်အရာကို ပို့မည်၊ မည်သည့်နေရာသို့ ပို့မည်ကို ဆုံးဖြတ်သည်။ Result processing system သည် messages များကို local GUI သို့မဟုတ် web interface သို့ ပို့နိုင်သည်။

**Datafeed Sourcing**  
Algorithmic trading engine အတွက် လိုအပ်သော data ကို ချိတ်ဆက်ပြီး download လုပ်သည့် IDataFeed။ Backtesting အတွက် disk မှ files များကို ရယူပြီး live trading အတွက် stream တစ်ခုသို့ ချိတ်ဆက်ကာ data objects များကို ထုတ်ပေးသည်။

**Transaction Processing**  
Order requests အသစ်များကို process လုပ်သည့် ITransactionHandler။ Algorithm မှ fill models များ သို့မဟုတ် အမှန်တကယ် brokerage ကိုအသုံးပြု၍ လုပ်ဆောင်သည်။ Processed orders များကို algorithm ၏ portfolio သို့ fill လုပ်ရန်ပြန်ပို့သည်။

**Realtime Event Management**  
Real-time events များ (ဥပမာ - end of day events) ထုတ်လုပ်ပေးသည့် IRealtimeHandler။ Realtime event handlers များသို့ callback များကို trigger လုပ်သည်။ Backtesting အတွက် simulated time ပေါ်တွင် အလုပ်လုပ်ရန် mock-up လုပ်ထားသည်။

**Algorithm State Setup**  
Algorithm cash, portfolio နှင့် data တောင်းခံမှုကို configure လုပ်သည့် ISetupHandler။ လိုအပ်သော state parameters အားလုံးကို initialize လုပ်သည်။

၎င်းတို့အားလုံးကို Launcher Project အတွင်းရှိ config.json ဖိုင်မှ configure လုပ်နိုင်သည်။

### Developing with Lean CLI
QuantConnect သည် local algorithm development အတွက် Lean CLI ကိုအသုံးပြုရန် အကြံပြုသည်။ ၎င်းသည် သင်၏ algorithms များကို local တွင် အလုပ်လုပ်စေပြီး cloud သို့ deploy လုပ်နိုင်ကာ Lean data ကို access ရှိစေသောကြောင့် အကောင်းဆုံး tool တစ်ခုဖြစ်သည်။ ထို့အပြင် တရားဝင် docker images များမှတစ်ဆင့် သင်၏ local machine ပေါ်တွင် သင်၏ data ဖြင့် algorithms များကို run နိုင်သည်။

Lean CLI အကြောင်း QuantConnect ၏ documentation ကို [ဤနေရာတွင်](https://www.quantconnect.com/docs/) ရယူနိုင်သည်။

### Installation Instructions
ဤအပိုင်းသည် သင့်ကိုယ်ပိုင်ပတ်ဝန်းကျင်တွင် အသုံးပြုရန် Lean ကို local ထည့်သွင်းနည်းကို ဖော်ပြပေးမည်။

သင်၏ local IDE ဖြင့် Lean အသုံးပြုခြင်းဆိုင်ရာ အသေးစိတ်လမ်းညွှန်ချက်များအတွက် အောက်ပါ readme ဖိုင်များကို ဖတ်ရှုပါ:
- VS Code
- VS

Local တွင်ထည့်သွင်းရန် နောက်ဆုံး master zip ဖိုင်ကို download လုပ်ပြီး သင်နှစ်သက်ရာနေရာတွင် unzip လုပ်ပါ။ သို့မဟုတ် Git ကို install လုပ်ပြီး repo ကို clone လုပ်ပါ:

```
$ git clone https://github.com/QuantConnect/Lean.git
$ cd Lean
```

**Mac OS**  
Visual Studio for Mac ကို ရပ်ဆိုင်းလိုက်ပြီဖြစ်၍ Visual Studio Code ကို အသုံးပြုပါ။  
1. Visual Studio Code for Mac ကို install လုပ်ပါ။  
2. C# Dev Kit extension ကို install လုပ်ပါ။  
3. dotnet 9 SDK ကို install လုပ်ပါ။  
4. LEAN directory ကို Visual Studio Code တွင် ဖွင့်ပါ။  
Solution ကို run ရန်:  
- Activity Bar မှ Run and Debug ကိုရွေးပါ  
- F5 နှိပ်ပါ  
- Command line မှ:  
  ```
  $ dotnet build QuantConnect.Lean.sln
  $ cd Lean/Launcher/bin/Debug
  $ dotnet QuantConnect.Lean.Launcher.dll
  ```

**Linux (Debian, Ubuntu)**  
1. dotnet 6 ကို install လုပ်ပါ။  
2. Lean Solution ကို compile လုပ်ပါ:  
   ```
   $ dotnet build QuantConnect.Lean.sln
   ```
3. Lean ကို run ပါ:  
   ```
   $ cd Launcher/bin/Debug
   $ dotnet QuantConnect.Lean.Launcher.dll
   ```

Interactive Brokers integration ကို set up လုပ်ရန် config.json ထဲရှိ `ib-tws-dir` နှင့် `ib-controller-dir` fields များကို TWS နှင့် IBController folders များ၏ အမှန်တကယ် paths များဖြင့် ပြင်ဆင်ပေးပါ။ အားလုံးပြီးသော်လည်း connection refuse error တက်နေသေးပါက config.json ရှိ `ib-port` field ကို 4002 မှ 4001 သို့ ပြောင်းပြီး သင်၏ IBGateway/TWS ရှိ settings နှင့် ကိုက်ညီစေရန် ကြိုးစားပါ။

**Windows**  
1. Visual Studio ကို install လုပ်ပါ။  
2. QuantConnect.Lean.sln ကို Visual Studio တွင် ဖွင့်ပါ။  
3. Build Menu -> Build Solution ဖြင့် solution ကို build လုပ်ပါ။  
4. F5 နှိပ်၍ run ပါ။

### Python Support
Python installation process ၏ အပြည့်အစုံရှင်းပြချက်ကို Algorithm.Python project တွင် တွေ့နိုင်သည်။

### Local-Cloud Hybrid Development
သင်၏ စိတ်ကြိုက် development environment တွင် local ၌ seamless စွာ develop လုပ်နိုင်ပြီး autocomplete နှင့် debugging support အပြည့်အဝဖြင့် ပြဿနာများကို လျင်မြန်စွာရှာဖွေနိုင်သည်။ အသေးစိတ်အတွက် CLI documentation ကို ကြည့်ပါ။

## Roadmap
ကျွန်ုပ်တို့၏ Roadmap သည် community အဖွဲ့ဝင်များထံမှ အာရုံစိုက်မှုအရဆုံး feature requests နှင့် bugs များကို ပြသပေးသည်။ Core QuantConnect အဖွဲ့သည် မဲအများဆုံးရသည့် feature requests နှင့် bugs များကို ဦးစားပေးသည်။ သင်သည် QuantConnect နှင့် LEAN ၏ အနာဂတ်ကို ပုံဖော်လိုပါက ယနေ့ပင် မဲပေးပါ။ Roadmap တွင် item အသစ်တစ်ခုထည့်ရန် LEAN repository တွင် GitHub Issue အသစ်တစ်ခုဖန်တီးပြီး thumbs up emoji ဖြင့် တုံ့ပြန်ပါ။

## Sponsorships
QuantConnect ကို sponsor လုပ်ခြင်းဖြင့် ကျွန်ုပ်တို့ developers များကို တော်လှန်ပြောင်းလဲနေသော quantitative trading platform LEAN ကို ပွင့်လင်း၊ ပူးပေါင်းဆောင်ရွက်သည့်နည်းဖြင့် မြှင့်တင်ရန် ထောက်ပံ့ပေးပါသည်။ ကျွန်ုပ်တို့သည် industry-grade tools နှင့် data accessibility ဖြင့် ကစားကွက်ကို ဆက်လက်အဆင့်မြှင့်တင်သွားမည်ဖြစ်သည်။ Sponsorship ရန်ပုံငွေကို အောက်ပါရည်မှန်းချက်များအောင်မြင်ရန် အသုံးပြုသည်:

- LEAN ၏ အခြေခံအဆောက်အအုံ ဖွံ့ဖြိုးတိုးတက်မှုကို ဆက်လက်လုပ်ဆောင်ရန်
- အခမဲ့၊ အရည်အသွေးမြင့် သုတေသနနှင့် ပညာပေး material များဖန်တီးရန်
- ကျွန်ုပ်တို့၏ community အတွက် ဆက်လက်ပံ့ပိုးမှုပေးရန်
- Dataset Market တွင် terabytes နှင့်ချီသော data များကို access ရရှိစေရန်
- LEAN ကို ကမ္ဘာ့ဘဏ္ဍာရေးဈေးကွက်များသို့ ယူဆောင်လာရန်
- Live trading brokerage connections များတိုးမြှင့်ရန်
- တစ်ဦးချင်းစီသည် ၎င်းတို့၏ ideas များအတွက် ဝင်ငွေရရှိနိုင်ရန် ဘဏ္ဍာရေးအဖွဲ့အစည်းများနှင့် ချိတ်ဆက်ပေးရန်

QuantConnect sponsor ဖြစ်လာရန် GitHub ရှိ [Sponsorship page](https://github.com/sponsors/QuantConnect) ကိုကြည့်ပါ။

---

## Contributions

### Datasets

#### Key Concepts

**Introduction**  
LEAN သို့ လှူဒါန်းထားသော Datasets များကို QuantConnect Dataset Marketplace တွင် လျင်မြန်စွာ စာရင်းသွင်းနိုင်ပြီး QuantConnect community ရှိ အသုံးပြုသူ ၂၅၀,၀၀၀ ကျော်ထံ ရောင်းချရန် ဖြန့်ဝေနိုင်သည်။ Dataset တစ်ခုစာရင်းသွင်းရန် QuantConnect Team ကို ဆက်သွယ်၍ အမြန်ပြန်လည်သုံးသပ်မှုပြုလုပ်ပြီးနောက် အောက်ပါစာမျက်နှာများရှိ data creation နှင့် process အဆင့်များအတိုင်း ဆက်လက်လုပ်ဆောင်ပါ။

Datasets များသည် ကောင်းစွာသတ်မှတ်ထားရမည်ဖြစ်ပြီး data ရရှိနိုင်ချိန် ("point in time") အတွက် လက်တွေ့ကျသော timestamps များရှိရမည်။ အကောင်းဆုံးအားဖြင့် datasets များသည် အနည်းဆုံး ၂ နှစ်စာ မှတ်တမ်းရှိပြီး ဂုဏ်သိက္ခာရှိသော ကုမ္ပဏီမှ ထိန်းသိမ်းထားရမည်။ ၎င်းတို့တွင် community မှ data ကိုအသုံးချနိုင်ရန် documentation အပြည့်အစုံနှင့် code examples များပါရှိသင့်သည်။

**Data Sources**  
သင်၏ dataset class ၏ `get_source` method သည် LEAN အား data ကိုမည်သည့်နေရာတွင်ရှာရမည်ကို ညွှန်ကြားသည်။ ဤ method သည် data တည်နေရာနှင့် format ပါဝင်သော `SubscriptionDataSource` object ကို return ပြန်ရမည်။ ကျွန်ုပ်တို့သည် သင်၏ data ကို host လုပ်ပေးသောကြောင့် `transport_medium` သည် `SubscriptionTransportMedium.LocalFile` ဖြစ်ရမည်ဖြစ်ပြီး format သည် `FileFormat.Csv` ဖြစ်ရမည်။

**TimeZones**  
သင်၏ data source class ၏ `DataTimeZone` method သည် သင်၏ dataset ၏ time zone ကို ကြေညာသည်။ ဤ method သည် `NodaTime.DateTimeZone` object ကို return ပြန်သည်။ သင်၏ dataset သည် trading data နှင့် universe data များကိုပေးအပ်ပါက `Lean.DataSource.<vendorNameDatasetName>/<vendorNameDatasetName>.cs` နှင့် `Lean.DataSource.<vendorNameDatasetName>/<vendorNameDatasetName>Universe.cs` ဖိုင်များရှိ `DataTimeZone` method များသည် တူညီရမည်။

**Linked Datasets**  
အောက်ပါအချက်များထဲမှ တစ်ခုမှန်ကန်ပါက သင်၏ dataset သည် linked ဖြစ်သည်:
- သင်၏ dataset သည် သတ်မှတ်ထားသော securities များ၏ market price properties များကို ဖော်ပြသည် (ဥပမာ၊ AAPL ၏ closing price)။
- သင်၏ alternative dataset သည် တစ်ဦးချင်း securities များနှင့် ချိတ်ဆက်ထားသည် (ဥပမာ၊ AAPL ၏ Wikipedia page view count)။

Linked မဟုတ်သော datasets များ၏ ဥပမာများမှာ New York City ၏ weather ဖြစ်ပြီး data သည် သတ်မှတ်ထားသော security နှင့် သက်ဆိုင်မှုမရှိပါ။

Dataset linked ဖြစ်သောအခါ ၎င်းသည် အချိန်နှင့်အမျှ underlying assets များသို့ map လုပ်ရန် လိုအပ်သည်။ `RequiresMapping` boolean သည် security နှင့် ticker mapping issues များကို LEAN မှ ကိုင်တွယ်ရန် ညွှန်ကြားသည်။

#### Defining Data Models

**Introduction**  
ဤစာမျက်နှာသည် data source SDK ကို set up လုပ်နည်းနှင့် data models များဖန်တီးရန် ၎င်းကိုအသုံးပြုပုံကို ရှင်းပြထားသည်။

**Part 1/ Set up SDK**  
သင်၏ dataset အတွက် repository တစ်ခုဖန်တီးရန် ဤအဆင့်များကို လိုက်နာပါ:

1. Lean.DataSource.SDK repository ကိုဖွင့်ပြီး `Use this template` > `Create a new repository` ကိုနှိပ်ပါ။
2. Create a new repository from Lean.DataSource.SDK စာမျက်နှာတွင် repository name ကို `Lean.DataSource.<vendorNameDatasetName>` (ဥပမာ၊ `Lean.DataSource.XYZAirlineTicketSales`) ဟုသတ်မှတ်ပါ။ သင်၏ dataset တွင် series အများအပြားပါဝင်ပါက `<vendorNameDatasetName>` အစား `<vendorName>` ကိုသုံးပါ။ ဥပမာ၊ Federal Reserve Economic Data (FRED) dataset repository တွင် မတူညီသော series များစွာပါဝင်သောကြောင့် နာမည်မှာ `Lean.DataSource.FRED` ဖြစ်သည်။
3. `Create repository from template` ကိုနှိပ်ပါ။
4. Lean.DataSource.<vendorNameDatasetName> repository ကို clone လုပ်ပါ:
   ```
   $ git clone https://github.com/username/Lean.DataSource.<vendorNameDatasetName>.git
   ```
5. အကယ်၍ Linux terminal ဖြစ်ပါက၊ သင်၏ `Lean.DataSource.<vendorNameDatasetName>` directory ထဲတွင် bash script ၏ access permissions ကိုပြောင်းပါ။
6. သင်၏ `Lean.DataSource.<vendorNameDatasetName>` directory တွင် `renameDataset.sh` bash script ကို run ပါ။
   ```
   $ renameDataset.sh
   ```
   Bash script သည် `Lean.DataSource.<vendorNameDatasetName>` directory အတွင်းရှိ placeholder text အချို့ကို သင်၏ dataset ၏ `<vendorNameDatasetName>` နှင့်အစားထိုးပြီး အချို့ဖိုင်များကို ပြန်လည်အမည်ပေးသည်။

**Part 2/ Create Data Models**  
သင်၏ model အတွက် input သည် chronological order ဖြင့် စီထားသော CSV ဖိုင်တစ်ခု သို့မဟုတ် အများအပြား ဖြစ်သင့်သည်။

```
1997-01-01, 905.2, 941.4, 905.2, 939.55, 38948210, 978.21
1997-01-02, 941.95, 944, 925.05, 927.05, 49118380, 1150.42
...
```

အကယ်၍ ဤ CSV ဖိုင်များ မရှိသေးပါက နောက်ပိုင်း Rendering Data အပိုင်းတွင် ဖန်တီးပါမည်။ ဤအဆင့်အတွက် format နှင့် requirements များသတ်မှတ်ရန် "toy example" ဖိုင်ကို အသုံးပြုရန် စဉ်းစားပါ။

Data source class ကို သတ်မှတ်ရန် အောက်ပါအဆင့်များကို လိုက်နာပါ:
1. `Lean.DataSource.<vendorNameDatasetName>/<vendorNameDatasetName>.cs` ဖိုင်ကိုဖွင့်ပါ။
2. သင်၏ dataset ၏ properties များကို သတ်မှတ်ပါ:
   - သင်၏ dataset တွင်ရှိသလောက် properties များအတွက် lines 32-36 ကို duplicate လုပ်ပါ။
   - `SomeCustomProperty` properties များကို သင်၏ dataset properties အမည်များ (ဥပမာ၊ `Destination`) သို့ ပြောင်းလဲပါ။
   - Streaming dataset ဖြစ်ပါက `ProtoMember` argument များကို 10 မှစပြီး တစ်ခုချင်းစီ တိုးပေးပါ။
   - Streaming dataset မဟုတ်ပါက `ProtoMember` property decorators များကို ဖျက်ပါ။
   - "Some custom data property" comments များကို သင်၏ dataset ရှိ property တစ်ခုချင်းစီ၏ ဖော်ပြချက်ဖြင့် အစားထိုးပါ။
3. သင်၏ dataset တွင် series အများအပြားပါဝင်ပါက (ဥပမာ FRED dataset) `Lean.DataSource.<vendorNameDatasetName>` directory တွင် series name ကို series code သို့ map လုပ်ရန် helper class ဖိုင်တစ်ခုဖန်တီးပါ။ ဥပမာအပြည့်အစုံအတွက် Lean.DataSource.FRED repository ရှိ `LIBOR.cs` ဖိုင်ကိုကြည့်ပါ။
4. `GetSource` method ကို သင်၏ dataset ဖိုင်(များ)၏ path ကိုညွှန်ပြရန် သတ်မှတ်ပါ။ Dataset သည် CSV ဖိုင်အများအပြားခွဲထားပါက `config.Symbol.Value` string ကိုအသုံးပြု၍ file path တည်ဆောက်ပါ။
5. `Reader` method ကို သင်၏ dataset class ၏ instances များ return ပြန်ရန် သတ်မှတ်ပါ။ `Symbol = config.Symbol` သတ်မှတ်ပြီး `end_time` ကို data point ကို ပထမဆုံး consume လုပ်နိုင်သည့်အချိန်သို့ သတ်မှတ်ပါ။
6. `DataTimeZone` method ကို သတ်မှတ်ပါ။
   ```csharp
   public override DateTimeZone DataTimeZone(){ return DateTimeZone.Utc; }
   ```
   `using QuantConnect;` ဖြင့် `TimeZones` class မှ helper attributes များကိုသုံးနိုင်သည်။ ဥပမာ `TimeZones.Utc` သို့မဟုတ် `TimeZones.NewYork`။
7. `SupportedResolutions` method ကိုသတ်မှတ်ပါ။
   ```csharp
   public override List<Resolution> SupportedResolutions(){ return DailyResolution; }
   ```
8. `DefaultResolution` method ကိုသတ်မှတ်ပါ။ အဖွဲ့ဝင်တစ်ဦးမှ resolution မသတ်မှတ်ပါက `DefaultResolution` ကိုအသုံးပြုသည်။
9. `IsSparseData` method ကိုသတ်မှတ်ပါ။ Tick resolution မဟုတ်ဘဲ အနည်းဆုံး sample တစ်ခုအတွက် data ပျောက်ဆုံးနေပါက sparse ဖြစ်သည်။ Sparse ဖြစ်လျှင် missing files အတွက် logging ကို disable လုပ်သည်။
10. `RequiresMapping` method ကိုသတ်မှတ်ပါ။ Linked dataset ဖြစ်ပါက `true` return ပြန်ပါ။
11. `Clone` method ကိုသတ်မှတ်ပါ။
12. `ToString` method ကိုသတ်မှတ်ပါ။

**Part 3/Create Universe Models**  
အကယ်၍ သင်၏ dataset သည် universe data မပေးပါက:
1. `Lean.DataSource.<vendorNameDatasetName>/<vendorNameDatasetName>Universe.cs` ဖိုင်ကိုဖျက်ပါ။
2. `Lean.DataSource.<vendorNameDatasetName>/<vendorNameDatasetName>UniverseSelectionAlgorithm.*` ဖိုင်များကိုဖျက်ပါ။
3. `tests/Tests.csproj` ဖိုင်မှ line 8 ကိုဖျက်ပါ။
4. ဤစာမျက်နှာ၏ ကျန်အပိုင်းကို ကျော်သွားပါ။

Universe data အတွက် input သည် CSV ဖိုင်များစွာဖြစ်ပြီး ပထမ column သည် security identifier ဖြစ်ကာ ဒုတိယ column သည် point-in-time ticker ဖြစ်ရမည်။

```
A R735QTJ8XC9X,A,17.19,109700,1885743,False,0.9904858,1
AA R735QTJ8XC9X,AA,71.25,513400,36579750,False,0.3992678,0.750075
...
```

Universe data source class ကိုသတ်မှတ်ရန်:
1. `Lean.DataSource.<vendorNameDatasetName>/<vendorNameDatasetName>Universe.cs` ဖိုင်ကိုဖွင့်ပါ။
2. Properties များကိုသတ်မှတ်ပါ။
3. `GetSource` method ကို ရက်စွဲ parameter ကို အသုံးပြု၍ file path ညွှန်ပြရန် သတ်မှတ်ပါ။
4. Reader method သည် universe class instances များကို return ပြန်ရမည်။ ပထမ column သည် security identifier၊ ဒုတိယ column သည် point-in-time ticker ဖြစ်ရပါမည်။ `new Symbol(SecurityIdentifier.Parse(csv[0]), csv[1])` ဖြင့် Symbol ဖန်တီးပါ။
5. `DataTimeZone` method ကိုသတ်မှတ်ပါ။
6. `SupportedResolutions` သည် အနည်းဆုံး hourly သို့မဟုတ် daily ဖြစ်ရမည်။
7. `DefaultResolution` သတ်မှတ်ပါ။
8. `IsSparseData` သတ်မှတ်ပါ။
9. `RequiresMapping` သတ်မှတ်ပါ။
10. `Clone` method သတ်မှတ်ပါ။
11. `ToString` method သတ်မှတ်ပါ။

#### Rendering Data

**Rendering Data with Python**  
ဤစာမျက်နှာသည် QuantConnect distribution အတွက် Python ဖြင့် dataset ကို download လုပ်ပြီး process လုပ်သည့် script ဖန်တီးနည်းကို ရှင်းပြသည်။

**Using Processing Framework**  
ဤအဆင့်တွင် `Lean.DataSource.<vendorNameDatasetName>/DataProcessing/process.py` ဖိုင်ကို ပြင်ဆင်ပြီး သင်၏ raw data ကို `GetSource` method များမျှော်လင့်သည့် format နှင့် တည်နေရာသို့ ပြောင်းလဲရွှေ့ပြောင်းရမည်။ Script သည် data history အားလုံးကို root directory ရှိ `output` directory (ဥပမာ၊ `C:/output`) တွင် သိမ်းဆည်းပြီး data history ၏ sample ကို `Lean.DataSource.<vendorNameDatasetName>/output` directory တွင် သိမ်းဆည်းရမည်။

အောက်ပါအဆင့်များကို လိုက်နာပါ:
1. `Lean.DataSource.<vendorNameDatasetName>/output` directory ၏ structure ကို `get_source` methods တွင်သတ်မှတ်ထားသော path structure နှင့်ကိုက်ညီအောင်ပြောင်းပါ (ဥပမာ `output/alternative/xyzairline/ticketsales`)။
2. `process.py` တွင် dataset တစ်ခုလုံး process လုပ်ရန်ကြာချိန်နှင့် တစ်ရက်စာ data update လုပ်ရန်ကြာချိန်တို့ကို တိုင်းတာရန် code ထည့်ပါ။ ဤအချက်အလက်သည် data documentation အတွက် လိုအပ်သည်။
3. Raw data ကို source မှ load လုပ်ပါ။ Data ကို period အလိုက် load လုပ်ပြီး process လုပ်သင့်သည်။ Script သို့ပေးထားသော date range ကိုအသုံးပြုပါ။
4. Universe selection data ဖြစ်ပြီး hourly resolution ထက်ပိုမြင့်ပါက hourly သို့မဟုတ် daily resolution သို့ resample လုပ်ပါ။
5. အောက်ပါအချက်များမှန်ကန်ပါက ကျန်အဆင့်များကို ကျော်သွားပါ:
   - Dataset သည် Equities နှင့် မသက်ဆိုင်ပါ။
   - Dataset သည် Equities နှင့်သက်ဆိုင်ပြီး point-in-time tickers များပါဝင်ပြီးသားဖြစ်ပါ။
6. Equities နှင့်သက်ဆိုင်ပြီး ticker changes များအတွက် ထည့်သွင်းစဉ်းစားထားခြင်းမရှိပါက point-in-time tickers ဖြစ်လာစေရန် အောက်ပါအဆင့်များက ကူညီပေးပါမည်။ US Equity Security Master dataset မရှိပါက ကျွန်ုပ်တို့ကို ဆက်သွယ်ပါ။
7. `DataProcessing/Program.cs` မှ `Main` method ၏ statements များကိုဖယ်ရှားပါ။
8. Data processing project ကို compile လုပ်ပါ: `$ dotnet build .\DataProcessing\DataProcessing.csproj`
9. `process.py` တွင် `from CLRImports import *` ထည့်ပါ။
10. Map file provider ဖန်တီးပြီး initialize လုပ်ပါ:
    ```python
    map_file_provider = LocalZipMapFileProvider()
    map_file_provider.Initialize(DefaultDataProvider())
    ```
11. Security identifier ဖန်တီးပါ:
    ```python
    sid = SecurityIdentifier.generate_equity(point_in_time_ticker, Market.USA, True, map_file_provider, csv_date)
    ```
12. `process.py` script ကို `DataProcessing/bin/debug/net9.0/` directory သို့ကူးယူပါ။
13. Script ကို run ပါ:
    ```
    $ cd DataProcessing/bin/debug/net9.0/
    $ python process.py
    ```
မှတ်ချက်: နောက်ဆုံး pull request တွင် ပြန်လည်သုံးသပ်နိုင်ရန်နှင့် demonstration algorithms run ရန်အတွက် sample data ပါဝင်ရမည်။

**Python Processor ဥပမာများ**  
- Lean.DataSource.BitcoinMetadata
- Lean.DataSource.BrainSentiment
- Lean.DataSource.CryptoSlamNFTSale
- Lean.DataSource.QuiverQuantTwitterFollowers
- Lean.DataSource.Regalytics

**Rendering Data with CSharp**  

**Introduction**  
ဤစာမျက်နှာသည် QuantConnect distribution အတွက် C# ဖြင့် dataset ကို download လုပ်ပြီး process လုပ်သည့် script ဖန်တီးနည်းကို ရှင်းပြသည်။

**Using Processing Framework**  
`Lean.DataSource.<vendorNameDatasetName>/DataProcessing/Program.cs` ဖိုင်ကို ပြင်ဆင်ရမည်။  
အဆင့်များမှာ Python နှင့် ဆင်တူပြီး map file provider ဖန်တီးချိန်တွင် C# syntax ကိုအသုံးပြုသည်။  
Compile လုပ်ပြီး `process.exe` ကို run ပါ။ Sample data ပါဝင်ရမည်။

**CSharp Processor ဥပမာများ**  
- Lean.DataSource.BinanceFundingRate
- Lean.DataSource.CoinGecko
- Lean.DataSource.CryptoCoarseFundamentalUniverse
- Lean.DataSource.QuiverInsiderTrading
- Lean.DataSource.VIXCentral

**Rendering Data with Notebooks**  

**Introduction**  
ဤစာမျက်နှာသည် Jupyter Notebooks ဖြင့် dataset ကို download လုပ်ပြီး process လုပ်နည်းကို ရှင်းပြသည်။

**Using Processing Framework**  
`process.ipynb` ဖိုင်ကို ပြင်ဆင်ရမည်။ Python script ကဲ့သို့ပင် data processing project ကို compile လုပ်ပြီး CLRImports ကို import လုပ်ကာ map file provider ဖန်တီးရမည်။ Cells များကို run ပြီး sample data ထုတ်ပေးရမည်။

**Notebook Processor ဥပမာများ**  
- Lean.DataSource.KavoutCompositeFactorBundle
- Lean.DataSource.USEnergy

#### Testing Data Models

ဤအဆင့်သည် သင်၏ dataset နှင့် demonstration algorithm ကို local LEAN ဖြင့် backtest လုပ်ပြီး unit tests များ run ခြင်းပါဝင်သည်။  
အကျဉ်းချုပ်အဆင့်များ:
1. Visual Studio တွင် `QuantConnect.DataSource.csproj` ကိုဖွင့်၍ build လုပ်ပါ။
2. LEAN repo ကို pull/clone လုပ်ပြီး data ဖိုင်များကို `Lean/Data` ထဲသို့ကူးထည့်ပါ။
3. Algorithm project ထဲသို့ dataset DLL ကို reference ထည့်ပါ။
4. C# နှင့် Python demonstration algorithms များရေးပြီး backtest run ပါ (error မရှိရ)။
5. Algorithm ဖိုင်များကို dataset repository သို့ကူးယူပါ။
6. Unit tests များရေးပြီး run ပါ။

#### Data Documentation

**Introduction**  
သင်၏ dataset အတွက် documentation ပေးအပ်ရန် ဤစာမျက်နှာက ရှင်းပြသည်။

**Required Key Properties**  
Dataset တစ်ခုလုံးကို process လုပ်ပြီး အောက်ပါအချက်အလက်များကို စုဆောင်းရမည်:
- Start Date (ပထမဆုံး data point ၏ ရက်စွဲနှင့်အချိန်)
- Asset Coverage (dataset မှ cover လုပ်သော assets အရေအတွက်)
- Data density (Tick data အတွက် Dense; frequency အရ Regular/Sparse)
- Resolution (Tick, Second, Minute, Hourly, Daily)
- Timezone (Data timezone)
- Data process time (Data ကို process လုပ်ရမည့် အချိန်နှင့် ရက်သတ္တပတ်ရက်များ)
- Data process duration (Dataset တစ်ခုလုံး process လုပ်ရန်ကြာချိန်)
- Update process duration (Dataset update လုပ်ရန်ကြာချိန်)

**Provide Documentation**  
`listing-about.md` နှင့် `listing-documentation.md` ဖိုင်များတွင် ပျောက်ဆုံးနေသော အကြောင်းအရာများကို ဖြည့်ပါ။

**Next Steps**  
ကျွန်ုပ်တို့ ပြန်လည်သုံးသပ်၍ လက်ခံပြီးနောက် Dataset Market တွင် စာမျက်နှာတစ်ခုဖန်တီးပေးမည်။ ထို့နောက်တွင် QuantConnect Cloud တွင် dataset ကိုအသုံးပြု၍ algorithms များရေးနိုင်ပြီး dataset listing အတွက် example algorithm တစ်ခုကိုလည်း လှူဒါန်းနိုင်သည်။

---

### Brokerages

Brokerage တစ်ခုကို အပြည့်အဝ support လုပ်ရန်မှာ စိန်ခေါ်မှုတစ်ခုဖြစ်သည်။ LEAN တွင် အစိတ်အပိုင်းတစ်ခုချင်းစီ အတူတကွအလုပ်လုပ်ပြီး ပြီးပြည့်စုံသော brokerage implementation တစ်ခုဖွဲ့စည်းရန် လိုအပ်သည်။ ဤလမ်းညွှန်သည် module တစ်ခုချင်းစီအတွက် သင်ဘာလုပ်ရမည်ကို တတ်နိုင်သမျှအသေးစိတ်ဖော်ပြရန် ရည်ရွယ်သည်။

အဆုံးပန်းတိုင်မှာ tests အားလုံးအောင်မြင်သော pull request တစ်ခုတင်ပြရန်ဖြစ်သည်။ တစ်စိတ်တစ်ပိုင်းပဲပြီးသော brokerage implementations များကို branch တစ်ခုသို့ merge လုပ်ရန်လည်း လက်ခံပါသည်။

Brokerage စနစ်၏ root မှာ algorithm job packets ဖြစ်ပြီး ၎င်းတွင် LEAN ကို run ရန် configuration information များပါဝင်သည်။ ပရိုဂရမ်လမ်းကြောင်းမှာ: config.json > create job packet > create brokerage factory matching name > set job packet brokerage data > factory creates brokerage instance ဖြစ်သည်။ ထို့ကြောင့် brokerage တစ်ခုကို root မှစတင်ဖန်တီးပါမည်။

#### Setting Up Your Environment
သင်၏ local brokerage repository ကို set up လုပ်ပါ။ (အသေးစိတ်အဆင့်များကို အပေါ်တွင်ဖော်ပြထားပြီး)

#### Laying the Foundation
`IBrokerageFactory` ကို stub ထုတ်ပြီး brokerage instance တစ်ခုကို initialize လုပ်ပါ။  
အဆင့်များ:
1. config.json တွင် brokerage configuration သော့များထည့်ပါ။
2. `BrokerageData` member ကို Config class မှ configuration များ load လုပ်ရန် update လုပ်ပါ။
3. `DefaultBrokerageModel` ကို inherit လုပ်ထားသော `BrokerageNameBrokerageModel.cs` ဖန်တီးပါ။
4. `GetBrokerageModel` ကို ထို model ကို return ပြန်ရန် သတ်မှတ်ပါ။
5. Websockets သုံးပါက `BaseWebsocketsBrokerage` ကို base class အဖြစ်သုံးပါ။
6. Constructor တွင် authentication data ကို private variable များအဖြစ် သိမ်းပါ။
7. `CreateBrokerage` method ကို သတ်မှတ်ပါ (မချိတ်ဆက်ဘဲ instance ဖန်တီးရန်)။
8. config.json တွင် `Live-<brokerageName>` environment key ထည့်ပါ။
9. Environment value ကို ထို environment သို့သတ်မှတ်ပါ။
10. Solution ကို build လုပ်ပါ။

#### Creating the Brokerage
`IBrokerage` တွင် brokerage ၏ core logic အများစုကို ထည့်သွင်းရေးသားရသည်။  
Brokerage သည် အောက်ပါအခန်းကဏ္ဍများကို ဆောင်ရွက်ရမည်:
1. Connection ထိန်းသိမ်းခြင်း
2. Algorithm portfolio, open orders, cashbook initialize လုပ်ခြင်း
3. Order များ create, update, cancel လုပ်ခြင်း
4. Order fill events လက်ခံခြင်းနှင့် portfolio တွင် apply လုပ်ခြင်း
5. Cash deposits/removals ကဲ့သို့ non-order events များကို ခြေရာခံခြင်း
6. Brokerage messages များကိုဘာသာပြန်ပြီး လိုအပ်သလိုလုပ်ဆောင်ခြင်း
7. History requests များကို ဆောင်ရွက်ပေးခြင်း

Implementation style: LEAN တွင် step-by-step implement လုပ်ရန် အကြံပြုသည်။ Test-driven development အတွက် `BrokerageTests.cs` base class မှ extend လုပ်နိုင်သည်။

- `Connect()`, `Disconnect()`, `IsConnected`, `PlaceOrder()`, `UpdateOrder()`, `CancelOrder()`, `GetOpenOrders()`, `GetAccountHoldings()`, `GetCashBalance()`, `GetHistory()` စသည့် method များကို implement လုပ်ရန် လိုအပ်သည်။

SDK Libraries: License ကောင်းပြီး .NET 6 နှင့်ကိုက်ညီပါက SDK ကို brokerage implementation ထဲသို့ ကူးထည့်နိုင်သည်။

#### Translating Symbol Conventions
`ISymbolMapper` ကိုအသုံးပြု၍ brokerage ၏ ticker များကို LEAN format သို့ ပြောင်းလဲပါ။

#### Describing Brokerage Limitations
`IBrokerageModel` ကိုအသုံးပြု၍ order အမျိုးအစားများ support မှုနှင့် transaction models များကို ဖော်ပြပါ။ (လမ်းညွှန်တည်ဆောက်ဆဲ)

#### Enabling Live Data Streaming
`IDataQueueHandler` ဖြင့် live streaming data service set up လုပ်ပါ။ (လမ်းညွှန်တည်ဆောက်ဆဲ)

#### Enabling Historical Data
`IHistoryProvider` ဖြင့် historical data API ကို အသုံးပြုပါ။ (လမ်းညွှန်တည်ဆောက်ဆဲ)

#### Downloading Data
`IDataDownloader` ဖြင့် data ကို LEAN format ဖြင့် disk သို့ သိမ်းဆည်းပါ။ (လမ်းညွှန်တည်ဆောက်ဆဲ)

#### Modeling Fee Structures
`IFeeModel` ဖြင့် တိကျသော fee structures ကို backtesting တွင် enable လုပ်ပါ။ (လမ်းညွှန်တည်ဆောက်ဆဲ)

#### Updating the Algorithm API
`ISecurityTransactionModel` ဖြင့် model အမျိုးမျိုးကို ပေါင်းစပ်၍ brokerage set တစ်ခုဖွဲ့စည်းပါ။ (လမ်းညွှန်တည်ဆောက်ဆဲ)

---

### Indicators

**Introduction**  
LEAN သည် လက်ရှိတွင် indicators ၁၀၀ ကျော်ကို support လုပ်သည်။ ဤစာမျက်နှာသည် open-source project သို့ indicator အသစ်တစ်ခု လှူဒါန်းနည်းကို ရှင်းပြသည်။

**Get Third-Party Values**  
တိကျမှုအတွက် third-party source များမှ တန်ဖိုးများကို ကိုးကားအဖြစ် ထည့်သွင်းရန်လိုအပ်သည်။ ဥပမာ TA-Lib, QuantLib ကဲ့သို့သော open-source projects များ၊ သို့မဟုတ် အလွန်ယုံကြည်ရသော websites များ။

**Define the Class**  
`Lean/Indicators` directory တွင် class ဖိုင်တစ်ခုထည့်ပါ။ Indicator သည် data point, bar, သို့မဟုတ် TradeBar indicator ဖြစ်နိုင်သည်။ အောက်ပါ properties များကို သတ်မှတ်ရမည်:
- `WarmUpPeriod` (int): တိကျသော indicator တန်ဖိုးအတွက် အနည်းဆုံး data entries အရေအတွက်။
- `IsReady` (bool): Indicator တွင် တန်ဖိုးထုတ်ရန် data လုံလောက်မှုရှိမရှိပြသည့် flag။

`ComputeNextValue` method ကိုလည်း implement လုပ်ရမည်။  
မမှန်ကန်သောတန်ဖိုးများအတွက် `ValidateAndComputeNextValue` ကို override လုပ်နိုင်သည်။  
Moving average လိုအပ်ပါက နောက်ဆုံးအဆင့် "Extra Steps for Moving Average Types" ကိုကြည့်ပါ။

Data point indicators များသည် `IndicatorBase<IndicatorDataPoint>` သို့မဟုတ် `WindowIndicator<IndicatorDataPoint>` ကို inherit လုပ်သည်။  
Bar indicators သည် `QuoteBar` သို့မဟုတ် `TradeBar` ကို အသုံးပြုသည်။  
TradeBar indicators သည် `TradeBar` ကို အသုံးပြုသည်။

**Define the Helper Method**  
`QCAlgorithm.Indicators.cs` တွင် automatic version အတွက် helper method တစ်ခုထည့်ပါ။

**Add Unit Tests**  
Third-party values ကို CSV အဖြစ် `Tests/TestData` တွင်သိမ်းပြီး test class ဖန်တီးပါ။ Constructor, IsReady, Reset method များကို စမ်းသပ်ပါ။

**Indicator Documentation**  
`IndicatorImageGenerator.py` တွင် indicator ကိုထည့်ပါ။ `indicator_reference_code_generator.py` ကို run ပြီး documentation စာမျက်နှာထုတ်ပါ။

**Extra Steps for Moving Average Types**  
`MovingAverageType` enum တွင် member အသစ်ထည့်ပါ။ `MovingAverageTypeExtensions.cs` နှင့် tests များတွင် case အသစ်ထည့်ပါ။

---

## Data Format

### Key Concepts

LEAN သည် open, human-readable data format ကိုအသုံးပြုရန် ကြိုးပမ်းထားပြီး flat files များမှ data ကိုဖတ်သည်။ Data compression ကို zip format ဖြင့်ပြုလုပ်ပြီး ဖိုင်များအားလုံးသည် CSV သို့မဟုတ် JSON ဖြစ်သည်။  
စျေးနှုန်းများကို asset quote currency ဖြင့်ဖော်ပြသည်။ Security တစ်ခုအတွက် activity မရှိလျှင် စျေးနှုန်းကိုဖိုင်မှ ချန်လှပ်ထားသည်။

**Folder Structure**  
- Tick, Second, Minute: `/data/securityType/marketName/resolution/ticker/date_tradeType.zip`
- Hour, Daily: `/data/securityType/marketName/resolution/ticker.zip`

`marketName` သည် တူညီသော ticker ဖြင့် ကွဲပြားသော tradable assets များကိုခွဲခြားရန် သုံးသည်။

### Core Data Types

**Trade Tick**  
Tick data သည် period မရှိပါ။ Columns: Time (milliseconds since midnight), Trade Sale (price), Quantity, Exchange, Trade Sale Condition, Suspicious (boolean)။  
TradeConditionFlags ဥပမာ REGULAR, FORM_T etc. (ဇယားတွင်ကြည့်ပါ)

**Quote Tick**  
Columns: Time, Bid Price, Ask Price, Bid Size, Ask Size, Exchange, Quote Sale Condition, Suspicious။  
QuoteConditionFlags ဥပမာ CLOSING, NEWS_DISSEMINATION, REGULAR (excluded), SLOW (excluded) etc.

**Trade Bar**  
Trade ticks များကို period တစ်ခုအတွင်း consolidate လုပ်ထားခြင်း။ Columns: Time, Open, High, Low, Close, Volume။

**Quote Bar**  
Top of book quote data ကို period တစ်ခုအတွင်း consolidate လုပ်ထားခြင်း။ Columns: Time, Bid Open, Bid High, Bid Low, Bid Close, Bid Size, Ask Open, Ask High, Ask Low, Ask Close, Ask Size။

**Open Interest**  
Columns: Time, Open Interest (outstanding contracts)။

---

## Statistics

### Capacity

Capacity သည် strategy တစ်ခုသည် market impact ကြောင့် performance မကျဆင်းမီ မည်မျှသော capital ကို trade လုပ်နိုင်သည်ကို တိုင်းတာခြင်းဖြစ်သည်။

**Security Capacity**  
Market Capacity Dollar Volume ကို bar များစွာကို ပေါင်းစပ်၍ တွက်ချက်သည်။ Crypto, Forex/CFD အတွက် မတူညီသော ခန့်မှန်းနည်းများရှိသည်။  
Volume Accumulation Period သည် asset liquidity ပေါ်မူတည်၍ resolution အလိုက် ဖော်မြူလာများရှိသည်။  
Available Portion of Market Capacity Dollar Volume သည် resolution အလိုက် ရာခိုင်နှုန်းကွဲပြားသည် (Daily 2%, Hour 5%, Minute 20%, Second/Tick 50%)။  
Fast Trading Volume Discount Factor သည် အကြိမ်ရေများစွာ trade လုပ်လေ capacity လျော့လေ ဖြစ်စေရန် discount factor ကိုအသုံးပြုသည်။  
Sale Volume ကိုလည်း ထည့်သွင်းစဉ်းစားသည်။

**Portfolio Capacity**  
အပတ်စဉ် snapshots ယူပြီး strategy capacity ကို အောက်ပါအတိုင်းတွက်ချက်သည်:
```
Snapshot Capacity = (Market Capacity Dollar Volume / Number Of Trades) / max(Sale Volume / Portfolio Sale Volume, Buying Power Used / Total Portfolio Value)
```
Denominator 0 ဖြစ်လျှင် quotient ကို 0 ဟုသတ်မှတ်သည်။  
နောက်ဆုံး strategy capacity ကို snapshot များကို အသုံးပြု၍ exponentially-weighted model ဖြင့် ချောမွေ့စေသည်:
```
Strategy Capacity = 0.66 * S_{i-1} + 0.33 * S_i
```

**Summary**  
ကြီးမားသော capacity ရှိသော strategies များသည် market impact မရှိဘဲ capital ပိုမို trade လုပ်နိုင်သည်။ Liquid securities များတွင် volume မြင့်မားစွာ trade လုပ်ခြင်းသည် capacity ကိုမြှင့်တင်ပေးသည်။

---

## Class Reference

QuantConnect API Reference သည် LEAN algorithmic trading framework ရှိ class, method, property, event အားလုံးကို အသေးစိတ်ဖော်ပြသည့် ပြည့်စုံသောနည်းပညာစာရွက်စာတမ်းဖြစ်သည်။ ၎င်းသည် syntax များကို လျင်မြန်စွာရှာဖွေရန်နှင့် ရရှိနိုင်သော features များကို စူးစမ်းရန် ကူညီပေးသည်။ LEAN engine ကို C# ဖြင့်ရေးသားထားသော်လည်း Python သို့မဟုတ် C# ဖြင့် algorithms များဖန်တီးနိုင်သည် (Python.Net ကိုအသုံးပြု၍)။ နှစ်မျိုးလုံးအတွက် API Reference ကို ရယူနိုင်ပါသည်။

[Python API Reference](https://www.quantconnect.com/docs/v2/lean-engine/class-reference)  
[C# API Reference](https://www.quantconnect.com/docs/v2/lean-engine/class-reference)
