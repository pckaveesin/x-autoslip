# X-AutoSlip (X-AUTO-SLIP-ANDROID)

A native Android application built with **Kotlin**, **Jetpack Compose (Material 3)**, **Google ML Kit Text Recognition**, and **Room Database** to automatically read bank transfer slips (สลิปธนาคาร), capture transaction amounts & currencies, auto-categorize expenses, track manual Income & Expense (รายรับ/รายจ่าย), and provide monthly financial summaries.

---

## Key Features

1. **Bank Slip OCR & Parsing (สแกนและอ่านสลิปธนาคาร)**
   - Select bank slip images directly from Android's **Picture / Gallery** folders using Android's modern Photo Picker (`PickVisualMedia`).
   - Uses **Google ML Kit On-Device OCR** (no external API keys or server required).
   - Automatically captures **Amount** (e.g. `1,250.00`, `350.00`) and detects **Currency** (`THB`, `บาท`, `฿`, `USD`, `EUR`, etc.).
   - Recognizes major Thai banks (KBank, SCB, Krungthai NEXT, Bangkok Bank, TTB, GSB, PromptPay) and extracts dates/times (with Buddhist Era BE -> CE conversion).

2. **Automatic Payment Categorization (จัดหมวดหมู่การชำระเงินอัตโนมัติ)**
   - Smart keyword rule engine that inspects payee names, slip notes, and merchant text.
   - Pre-configured Thai payment categories:
     - **Food & Dining (อาหารและเครื่องดื่ม)**: GrabFood, Lineman, 7-Eleven, Cafe Amazon, ร้านอาหาร, ก๋วยเตี๋ยว, ชาบู, ฯลฯ
     - **Fuel & Transport (น้ำมันและการเดินทาง)**: PTT Station, Shell, Bangchak, MRT, BTS, ทางด่วน, เติมน้ำมัน, Grab, ฯลฯ
     - **Shopping (ช้อปปิ้ง)**: Shopee, Lazada, TikTok Shop, Lotus, Big C, CJ Express, ฯลฯ
     - **Bills & Utilities (บิลและสาธารณูปโภค)**: การไฟฟ้านครหลวง/ส่วนภูมิภาค (MEA/PEA), การประปา, AIS, True, Internet, ฯลฯ
     - **Health & Medical (สุขภาพและยา)**: โรงพยาบาล, คลินิก, ร้านยา, Watsons, Boots, ฯลฯ
     - **Entertainment (บันเทิงและพักผ่อน)**: ตั๋วหนัง Major, SF, Netflix, Spotify, Steam, ฯลฯ

3. **Income / Expense Tracking (บันทึกรายรับ / รายจ่าย)**
   - Dedicated manual entry and edit screen with intuitive toggle tabs:
     - **Income (รายรับ)** - Highlighted in Emerald Green
     - **Expense (รายจ่าย)** - Highlighted in Coral Red
   - Support for custom currency selection (`THB`, `USD`, `EUR`, `JPY`, `SGD`), category tags, notes, and timestamp editing.

4. **Monthly Summary & Date-Based Grouping (สรุปรายเดือนและรวมยอดตามวัน)**
   - Month-by-month navigation and analytics dashboard:
     - **Total Income (รายรับรวม)**
     - **Total Expense (รายจ่ายรวม)**
     - **Net Balance (ยอดคงเหลือสุทธิ)**
   - Visual **Category Breakdown** with percentage progress bars.
   - Transactions grouped chronologically by date (e.g., Today, Yesterday, specific dates).

---

## Tech Stack & Architecture

- **Language**: Kotlin 2.0
- **UI Framework**: Jetpack Compose with Material 3 Design
- **Local Persistence**: Android Room Database (SQLite) with Coroutine Flows
- **OCR Engine**: Google ML Kit Text Recognition (`com.google.android.gms:play-services-mlkit-text-recognition`)
- **Image Loading**: Coil Compose (`io.coil-kt:coil-compose`)
- **Architecture**: Clean Architecture / MVVM (Model-View-ViewModel) + Repository Pattern
- **Internationalization**: Bilingual support (English & Thai)

---

## Project Structure

```
X-AUTO-SLIP-ANDROID/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── AndroidManifest.xml
│   │   │   ├── java/com/xautoslip/app/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── XAutoSlipApplication.kt
│   │   │   │   ├── data/
│   │   │   │   │   ├── local/ (Room AppDatabase, DAOs, Entities)
│   │   │   │   │   └── repository/ (TransactionRepository)
│   │   │   │   ├── domain/
│   │   │   │   │   ├── categorizer/ (AutoCategorizer rule engine)
│   │   │   │   │   ├── model/ (Transaction, Category, SlipParseResult, MonthlySummary)
│   │   │   │   │   ├── ocr/ (SlipOcrScanner with ML Kit)
│   │   │   │   │   └── parser/ (BankSlipParser)
│   │   │   │   └── ui/
│   │   │   │       ├── components/ (Summary Cards, Transaction Items, Headers)
│   │   │   │       ├── navigation/ (NavGraph, Screen routes, Bottom Navigation)
│   │   │   │       ├── screens/ (Dashboard, SlipScan, AddEdit, Monthly)
│   │   │   │       └── theme/ (Color, Theme, Typography)
│   │   │   └── res/
│   │   │       ├── values/ (English strings, colors)
│   │   │       └── values-th/ (Thai localized strings)
│   │   └── test/java/com/xautoslip/app/
│   │       ├── BankSlipParserTest.kt
│   │       └── AutoCategorizerTest.kt
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── gradle/
│   └── libs.versions.toml
├── build.gradle.kts
├── settings.gradle.kts
└── README.md
```

---

## How to Build and Run

1. Open the project in **Android Studio Hedgehog / Iguana / Jellyfish** (or later).
2. Ensure you have **JDK 17** configured in `Settings -> Build, Execution, Deployment -> Build Tools -> Gradle`.
3. Let Gradle sync dependencies.
4. Run on an Android device or emulator running **Android 7.0 (API 24)** or above (Recommended: Android 13+).

---

## Remote Repository

Azure DevOps:
```
https://dev.azure.com/x-devsolution/X-AUTO-SLIP/_git/X-AUTO-SLIP-ANDROID
```
