<div align="center">

# 📦 Paging3 Products

**A focused Jetpack Compose demo of a correct, production-grade Paging 3 implementation**

*یک پروژه‌ی متمرکز با Jetpack Compose برای نمایش یک پیاده‌سازی صحیح و آماده‌ی پروداکشن از Paging 3*

[![Kotlin](https://img.shields.io/badge/Kotlin-100%25-7F52FF?logo=kotlin&logoColor=white)](https://kotlinlang.org)
[![Jetpack Compose](https://img.shields.io/badge/UI-Jetpack%20Compose-4285F4?logo=jetpackcompose&logoColor=white)](https://developer.android.com/jetpack/compose)
[![Paging](https://img.shields.io/badge/Library-Paging%203-orange)]()
[![Ktor](https://img.shields.io/badge/Networking-Ktor-087CFA?logo=kotlin&logoColor=white)](https://ktor.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license--لایسنس)

</div>

---

## 🇬🇧 English

### Overview

**Paging3 Products** is a small, deliberately-scoped Android app built to demonstrate a **correct** end-to-end **Paging 3** implementation in Jetpack Compose — the kind of thing that comes up constantly in interviews and is very easy to get subtly wrong. It fetches paginated product data from the [DummyJSON](https://dummyjson.com/products) API using **Ktor** and renders it with full, explicit handling of every loading state Paging 3 exposes.

This isn't meant to be a full-featured app (no detail screen, no cart) — it's a focused reference implementation of one thing, done properly.

### ✨ What it actually gets right

- 📄 **Correct `PagingSource`** — `prevKey`/`nextKey` are derived from the real `skip`/`total` values returned by the API response, not guessed from the page size
- 🔑 **Correct `getRefreshKey()`** — properly recomputes the anchor position on refresh, a step that's frequently skipped or implemented incorrectly
- 💾 **`cachedIn(viewModelScope)`** — paged data survives configuration changes (e.g. screen rotation) without re-fetching
- 🧯 **Full `LoadState` coverage** — each of the four states is handled distinctly:
  - Initial load (full-screen loading indicator)
  - Initial load error (retryable, with a dedicated retry action)
  - Empty result state
  - Append (next-page) loading and append error, each with their own retry action, rendered inline at the bottom of the list
- 🌐 **Ktor** instead of Retrofit — a deliberate choice to demonstrate familiarity with Kotlin's multiplatform-friendly HTTP client
- 🧩 **Dagger Hilt** for DI (network client, repository, ViewModel)

### 🏗️ Architecture

```
ui/             →  Compose screen + ViewModel (exposes Flow<PagingData<Product>>)
      ↓
data/           →  Repository (wraps Pager/PagingSource)
      ↓
paging/         →  ProductPagingSource (talks to the DummyJSON API via Ktor)
```

### 🛠️ Tech Stack

| Category | Library / Tool |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose |
| Pagination | Paging 3 (`Pager`, `PagingSource`, `LoadState`) |
| Networking | Ktor Client, `kotlinx.serialization` |
| Dependency Injection | Dagger Hilt |
| Async | Kotlin Coroutines & Flow |

### 🚀 Getting Started

1. Clone the repository
   ```bash
   git clone https://github.com/<your-username>/paging3-products.git
   ```
2. Open the project in **Android Studio (Koala or newer)** and run it on API 26+

No API key needed — [DummyJSON](https://dummyjson.com) is a free, public REST API.

### 🗺️ Possible next steps

- Pull-to-refresh via `PullToRefreshBox` calling `pagingItems.refresh()`
- A product detail screen and search/category filtering (turning this into a full catalog app, similar to [CoffeeShop App](#))
- Friendlier, mapped error messages instead of raw exception text
- A `RemoteMediator` + Room layer for offline-first caching (see [Bulletin News](#) for that pattern)

### 📄 License / لایسنس

This project is licensed under the [MIT License](LICENSE).

---

## 🇮🇷 فارسی

### معرفی پروژه

**Paging3 Products** یک اپلیکیشن اندرویدی کوچک و عمداً محدود است که برای نمایش یک پیاده‌سازی **صحیح** و کامل از **Paging 3** در Jetpack Compose ساخته شده — چیزی که مدام توی مصاحبه‌های فنی پرسیده می‌شه و خیلی راحت می‌شه به‌شکل ظریفی اشتباه پیاده‌سازیش کرد. این پروژه داده‌ی صفحه‌بندی‌شده‌ی محصولات رو از API آزاد [DummyJSON](https://dummyjson.com/products) با **Ktor** می‌گیره و تمام حالت‌های لودینگی که Paging 3 در اختیار می‌ذاره رو به‌طور کامل و صریح مدیریت می‌کنه.

این پروژه قرار نیست یه اپ کامل باشه (نه صفحه‌ی جزئیات داره، نه سبد خرید) — بلکه یک پیاده‌سازی مرجع و متمرکز روی یک چیز خاصه، ولی درست انجام‌شده.

### ✨ چیزی که واقعاً درست پیاده شده

- 📄 **`PagingSource` صحیح** — مقادیر `prevKey`/`nextKey` از روی `skip`/`total` واقعی که API برمی‌گردونه محاسبه می‌شن، نه حدس‌زده‌شده از روی سایز صفحه
- 🔑 **`getRefreshKey()` صحیح** — موقعیت anchor رو موقع رفرش درست بازمحاسبه می‌کنه، قدمی که خیلی وقت‌ها یا فراموش می‌شه یا غلط پیاده‌سازی می‌شه
- 💾 **`cachedIn(viewModelScope)`** — داده‌ی صفحه‌بندی‌شده با تغییر پیکربندی (مثل چرخش صفحه) از بین نمی‌ره و دوباره fetch نمی‌شه
- 🧯 **پوشش کامل `LoadState`** — هر کدوم از چهار حالت جدا مدیریت شده:
  - لود اولیه (نشانگر لودینگ تمام‌صفحه)
  - خطای لود اولیه (قابل تلاش مجدد، با یک اکشن Retry اختصاصی)
  - حالت نتیجه‌ی خالی
  - لودینگ صفحه‌ی بعدی (append) و خطای append، هرکدوم با Retry جداگانه، نمایش داده‌شده به‌صورت inline پایین لیست
- 🌐 **Ktor به‌جای Retrofit** — یک انتخاب آگاهانه برای نشون‌دادن آشنایی با HTTP کلاینت سازگار با Kotlin Multiplatform
- 🧩 **Dagger Hilt** برای تزریق وابستگی (کلاینت شبکه، Repository، ViewModel)

### 🏗️ معماری

```
ui/             →  صفحه‌ی Compose + ViewModel (منتشرکننده‌ی Flow<PagingData<Product>>)
      ↓
data/           →  Repository (پوشش‌دهنده‌ی Pager/PagingSource)
      ↓
paging/         →  ProductPagingSource (ارتباط با API دیتابیس DummyJSON از طریق Ktor)
```

### 🛠️ استک فنی

| دسته | کتابخانه / ابزار |
|---|---|
| زبان | Kotlin |
| رابط کاربری | Jetpack Compose |
| صفحه‌بندی | Paging 3 (`Pager`, `PagingSource`, `LoadState`) |
| شبکه | Ktor Client، `kotlinx.serialization` |
| تزریق وابستگی | Dagger Hilt |
| Async | Kotlin Coroutines و Flow |

### 🚀 شروع به کار

۱. ریپازیتوری را کلون کنید:
```bash
git clone https://github.com/<your-username>/paging3-products.git
```
۲. پروژه را در **Android Studio (نسخه‌ی Koala یا جدیدتر)** باز کرده و روی API 26 به بالا اجرا کنید

نیازی به کلید API نیست — [DummyJSON](https://dummyjson.com) یک REST API آزاد و رایگان است.

### 🗺️ قدم‌های بعدی ممکن

- افزودن Pull-to-Refresh با `PullToRefreshBox` که `pagingItems.refresh()` رو صدا بزنه
- افزودن صفحه‌ی جزئیات محصول و جستجو/فیلتر دسته‌بندی (تبدیل به یک اپ کاتالوگ کامل، شبیه [CoffeeShop App](#))
- پیام‌های خطای کاربرپسند‌تر به‌جای متن خام اکسپشن
- افزودن لایه‌ی `RemoteMediator` + Room برای کش آفلاین-فرست (همون الگویی که توی [Bulletin News](#) پیاده شده)

### 📄 لایسنس

این پروژه تحت [مجوز MIT](LICENSE) منتشر شده است.

---

<div align="center">
Made with ❤️ using Kotlin & Jetpack Compose
</div>
