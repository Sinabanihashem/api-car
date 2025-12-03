# 🚗 SinaCarAPI — نسخه 1.0.0

وب‌سرویس **SinaCarAPI** یک API سریع، سبک و بدون نیاز به API Key برای دریافت **قیمت لحظه‌ای خودروهای داخلی و وارداتی** از منبع معتبر قیمت خودروها است.
این سرویس تمام اطلاعات شامل **برند، نام خودرو، قیمت بازار، قیمت کارخانه، میزان تغییرات، درصد تغییر و زمان بروزرسانی و...** را ارائه می‌دهد.  
دنبال وب‌سرویس قیمت خودرو میگردی ولی پیداش نمیکنی؟ پیدا کردی ولی رایگان نیست؟ از این وب‌سرویس بدون دردسر استفاده کن😊⚡

---

## 🌐 آدرس وب‌سرویس‌ها

| توضیح | لینک |
|------|-------|
| دریافت خودروهای داخلی | https://car.api-sina-free.workers.dev/cars?type=domestic |
| دریافت خودروهای وارداتی | https://car.api-sina-free.workers.dev/cars?type=imported |
| دریافت همه خودروها | https://car.api-sina-free.workers.dev/cars?type=all |

---

## 🔎 پارامتر ورودی

| پارامتر | مقدارهای قابل قبول | توضیح |
|---------|--------------------|--------|
| `type` | `domestic` / `imported` / `all` | تعیین نوع خودروها |

اگر مقدار وارد نشود → مقدار پیش‌فرض `domestic`

---

## 📦 ساختار خروجی

هر درخواست یک شیء JSON شامل موارد زیر برمی‌گرداند:

| پارامتر | نوع | توضیح |
|--------|------|--------|
| brand | string | برند تشخیص‌داده‌شده خودرو |
| name | string | نام دقیق خودرو |
| market_price | string | قیمت بازار |
| factory_price | string | قیمت کارخانه |
| change_percent | string | درصد تغییر (مثبت یا منفی) |
| change_value | string | مقدار تغییر قیمتی |
| last_update | string | زمان بروزرسانی به فرمت ISO |

---

## 🧪 نمونه درخواست

**GET**

https://car.api-sina-free.workers.dev/cars?type=all

---

## 🧾 نمونه خروجی

```json
{
  "type": "all",
  "cars": [
    {
      "brand": "ایران خودرو",
      "name": "پژو 207 اتوماتیک",
      "market_price": "1,240,000,000",
      "factory_price": "0",
      "change_percent": "۰%",
      "change_value": "0",
      "last_update": "2025-12-03T09:22:41.120Z"
    },
    {
      "brand": "Kia Motors",
      "name": "اسپورتیج (هرمس)",
      "market_price": "3,890,000,000",
      "factory_price": "0",
      "change_percent": "-0.3%",
      "change_value": "-10,000,000",
      "last_update": "2025-12-03T09:22:41.120Z"
    }
  ]
}
```

---

💻 نمونه استفاده در Python

```py
import requests

API = "https://car.api-sina-free.workers.dev/cars?type=imported"

res = requests.get(API)
cars = res.json()["cars"]

for c in cars:
    print("🚘 نام:", c["name"])
    print("🏷 برند:", c["brand"])
    print("💵 قیمت بازار:", c["market_price"])
    print("📉 تغییر:", c["change_percent"])
    print("⏱ بروزرسانی:", c["last_update"])
    print("-" * 30)
```

---

🤖 نمونه استفاده در ربات روبیکا / سایر بات‌ها

```py
from rubpy import Client, filters
import requests

bot = Client(name="sina_car_bot")
API_URL = "https://car.api-sina-free.workers.dev/cars?type=all"

def get_cars():
    try:
        res = requests.get(API_URL, timeout=5)
        return res.json().get("cars", [])
    except:
        return []

@bot.on_message_updates(filters.text)
async def handler(message):
    text = message.text.strip()

    if text == "قیمت خودرو":
        cars = get_cars()
        if not cars:
            return await message.reply("❗ خطا در دریافت اطلاعات.")

        output = "🚗 *قیمت لحظه‌ای خودروها:*\n\n"
        for c in cars[:10]:
            output += (
                f"🏷 *{c['name']}*\n"
                f"• برند: {c['brand']}\n"
                f"• بازار: {c['market_price']}\n"
                f"• تغییر: {c['change_percent']} ({c['change_value']})\n"
                f"• بروزرسانی: {c['last_update']}\n\n"
            )

        await message.reply(output, parse_mode="markdown")

bot.run()
```

---

🎯 مزایای SinaCarAPI

⚡ بسیار سریع

❌ بدون نیاز به API Key

♻️ بروزرسانی در هر درخواست

📊 دسته‌بندی کاملاً دقیق خودروها (داخلی / وارداتی)

🔍 تشخیص برند هوشمند با الگوریتم Match



---

👤 Developer

mir sina banihashem

📍 Hosted on: Cloudflare Workers
🛠 Rubika: https://rubika.ir/Sinabani_api
🔗 Endpoint: https://car.api-sina-free.workers.dev/cars

---
---

# 🚗 **SinaCarAPI — Version 1.0.0**

**SinaCarAPI** is a fast, lightweight, and free API that provides **real-time prices of domestic and imported cars in Iran** — without any API Key required.  
It delivers complete information including **brand detection, car name, market price, factory price, price changes, change percentage, update time, and more**.  
Looking for a car price API but can’t find one? Or found one but it's not free?  
Use this API with zero hassle! ⚡😊

---

## 🌐 **Available Endpoints**

| Description | URL |
|-------------|-----|
| Get domestic cars | https://car.api-sina-free.workers.dev/cars?type=domestic |
| Get imported cars | https://car.api-sina-free.workers.dev/cars?type=imported |
| Get all cars | https://car.api-sina-free.workers.dev/cars?type=all |

---

## 🔎 **Query Parameter**

| Parameter | Accepted Values | Description |
|----------|------------------|-------------|
| `type` | `domestic` / `imported` / `all` | Select category of cars |

If not provided → default value is `domestic`.

---

## 📦 **Response Structure**

Each request returns a JSON object containing:

| Field | Type | Description |
|--------|------|-------------|
| brand | string | Detected car brand |
| name | string | Car model name |
| market_price | string | Market price |
| factory_price | string | Factory price |
| change_percent | string | Percentage price change |
| change_value | string | Price change amount |
| last_update | string | Timestamp in ISO format |

---

## 🧪 **Sample Request**

**GET**

https://car.api-sina-free.workers.dev/cars?type=all

---

## 🧾 **Sample JSON Output**

```json
{
  "type": "all",
  "cars": [
    {
      "brand": "Iran Khodro",
      "name": "Peugeot 207 Automatic",
      "market_price": "1,240,000,000",
      "factory_price": "0",
      "change_percent": "0%",
      "change_value": "0",
      "last_update": "2025-12-03T09:22:41.120Z"
    },
    {
      "brand": "Kia Motors",
      "name": "Sportage (Hermes)",
      "market_price": "3,890,000,000",
      "factory_price": "0",
      "change_percent": "-0.3%",
      "change_value": "-10,000,000",
      "last_update": "2025-12-03T09:22:41.120Z"
    }
  ]
}
```

---

💻 Python Usage Example

```py
import requests

API = "https://car.api-sina-free.workers.dev/cars?type=imported"

res = requests.get(API)
cars = res.json()["cars"]

for c in cars:
    print("🚘 Name:", c["name"])
    print("🏷 Brand:", c["brand"])
    print("💵 Market Price:", c["market_price"])
    print("📉 Change:", c["change_percent"])
    print("⏱ Updated:", c["last_update"])
    print("-" * 30)
```

---

🤖 Rubika Bot Example (Python)

```py
from rubpy import Client, filters
import requests

bot = Client(name="sina_car_bot")
API_URL = "https://car.api-sina-free.workers.dev/cars?type=all"

def get_cars():
    try:
        res = requests.get(API_URL, timeout=5)
        return res.json().get("cars", [])
    except:
        return []

@bot.on_message_updates(filters.text)
async def handler(message):
    text = message.text.strip()

    if text == "قیمت خودرو":
        cars = get_cars()
        if not cars:
            return await message.reply("❗ خطا در دریافت اطلاعات.")

        output = "🚗 *Latest Car Prices:*\n\n"
        for c in cars[:10]:
            output += (
                f"🏷 *{c['name']}*\n"
                f"• Brand: {c['brand']}\n"
                f"• Market Price: {c['market_price']}\n"
                f"• Change: {c['change_percent']} ({c['change_value']})\n"
                f"• Updated: {c['last_update']}\n\n"
            )

        await message.reply(output, parse_mode="markdown")

bot.run()
```

---

🎯 Why Choose SinaCarAPI?

⚡ Super fast
❌ No API Key required
♻️ Fresh data on every request
📊 Accurate classification (Domestic / Imported)
🔍 Smart brand detection engine


---

👤 Developer

mir sina banihashem

📍 Hosted on: Cloudflare Workers
🛠 Rubika: https://rubika.ir/Sinabani_api
🔗 Endpoint: https://car.api-sina-free.workers.dev/cars
