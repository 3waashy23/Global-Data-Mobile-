# Somtel Global Data — eSIM SuperApp

## Project Overview
A fully client-side eSIM purchasing and management web app for **Somtel SuperApp**. Users can browse data plans by country or region, select packages, simulate payment, and receive a QR code for eSIM activation — all within a single-page mobile-first UI.

---

## ✅ Completed Features

### 🛒 Shop (Country & Region Browse)
- Search destinations by country name or region
- Toggle between **Country** and **Region** browsing modes
- Country cards show flag emoji, name, and starting price
- Region cards show globe icon, region name, country count pill, and starting price
- **Device compatibility checker** — detects iPhone, Android, iPad via User-Agent and advises eSIM support

### 📦 Package Selection
- Two package tiers per destination:
  - **1 GB · 7 Days** (weekly)
  - **10 GB · 30 Days** (monthly)
- Prices are per-country/region from embedded data
- Terms & Conditions checkbox gate before purchase
- Regional packages show a "Covered countries" drawer with search and sub-group breakdown (e.g. East Africa, Western Europe)

### 💳 Payment
- Order summary card (country, plan, validity, total)
- Payment method selection: **eDahab** (mobile wallet with PIN prompt) or **Visa/Mastercard**
- Animated processing overlay (spinner → success check)

### 📱 QR Code & Installation
- Auto-generated LPA activation string (`LPA:1$rsp.somtel.example$STL-…`)
- Live QR code rendered via **qrcodejs** (CDN)
- Activation code displayed as plain text fallback
- Step-by-step eSIM installation instructions

### 💼 My eSIMs
- Lists all eSIMs purchased during the session
- Shows plan, validity, remaining data, expiry
- "View QR" button reopens the QR/install page
- "Top Up" shortcut button

### 🔄 Top Up
- Lists active eSIMs with quick top-up buttons (1 GB or 10 GB)
- Goes directly to the payment page for the selected bundle

---

## 📂 File Structure
```
index.html      — Complete single-file app (HTML + CSS + JS)
README.md       — Project documentation
```

---

## 🔗 Entry Point
| Path | Description |
|------|-------------|
| `index.html` | Main app — opens on the Shop / Country list page |

---

## 📊 Data Models (embedded in JS)

### `countries[]`
| Field | Type | Description |
|-------|------|-------------|
| country | string | Country name |
| region | string | Region name (Africa, Asia, Europe, …) |
| weekly1gb | number | Price (USD) for 1 GB · 7 Days |
| monthly10gb | number | Price (USD) for 10 GB · 30 Days |

### `regions[]`
| Field | Type | Description |
|-------|------|-------------|
| region | string | Region name |
| weekly1gb | number | Regional price for 1 GB · 7 Days |
| monthly10gb | number | Regional price for 10 GB · 30 Days |
| countries | string[] | List of covered country names |

### `myEsims[]` (in-memory, session only)
Stores purchased eSIM objects: `{ country, flag, plan, validity, price, status, remaining, expiry }`

---

## 🌍 Supported Destinations (26 countries, 6 regions)
**Countries:** Anguilla, China, DR Congo, Ethiopia, France, Germany, India, Indonesia, Italy, Kenya, Malaysia, Netherlands, Netherlands Antilles, Oman, Republic of Congo, Saudi Arabia, South Africa, Sweden, Thailand, Turkey, U.S. Virgin Islands, Uganda, United Arab Emirates, United Kingdom, United States, Zambia

**Regions:** Africa · Americas · Asia · Europe · Middle East · Other

---

## 🔧 External Dependencies (CDN)
| Library | Purpose |
|---------|---------|
| [qrcodejs](https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js) | QR code generation for eSIM activation |

---

## ⚠️ Features Not Yet Implemented
- Real payment gateway integration (eDahab API, Stripe/card processor)
- Backend eSIM provisioning (real SM-DP+ server / LPA string from provider)
- User authentication & persistent order history (currently session-only)
- Push notifications for expiry reminders
- Multi-language / RTL support (Somali, Arabic)
- Admin dashboard for pricing management

## 🚀 Recommended Next Steps
1. Connect to a real eSIM provider API (e.g. Airalo, eSIM Go, or Somtel's own SM-DP+)
2. Add a backend for order records and payment confirmation webhooks
3. Integrate eDahab mobile-money API for live wallet payments
4. Add localStorage persistence so purchased eSIMs survive page refresh
5. Wrap as a PWA (manifest + service worker) for app-like mobile experience
