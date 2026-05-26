# Bokeo Transit Pro — Demo App Design Spec

## Overview

**App name:** ບໍ່ແກ້ວ Transit Pro
**Purpose:** Polished investor demo of a Lao-language transit booking app for Bokeo province.
**Tech:** Single HTML file with embedded CSS + vanilla JS. Zero dependencies. No backend.
**Data:** All fake/hardcoded. Demo only.

## Target

- Show to investors and clients
- Demonstrate modern mobile UI with Lao language and Lao cultural style
- Bokeo province routes only (Huay Xai, Ton Pheung, Paktha, Pha Oudom)

## Color & Style

| Token        | Value     | Usage                         |
|-------------|-----------|-------------------------------|
| Primary     | #1B7A3D   | Mekong green — buttons, headers, active tabs |
| Accent      | #D4A017   | Gold — icons, borders, highlights |
| Background  | #FFF8F0   | Light cream — page background |
| Card BG     | #FFFFFF   | White cards with subtle gold border |
| Text        | #1A1A1A   | Dark text                     |
| Text muted  | #6B7280   | Secondary text                |

**Lao pattern (ລາຍລາວ):** CSS decorative borders on headers inspired by Bokeo-style ລາຍນາກ (naga scale) and ລາຍຂໍ (hook/spiral) motifs from Lao Lue weaving tradition. Rendered as repeating stepped-diamond and hook patterns using CSS `linear-gradient` and `repeating-linear-gradient`. Colors: gold (#D4A017) on green (#1B7A3D) background.

**Typography:** System font stack with Lao Unicode support. Larger font sizes for Lao readability.

**Mobile frame:** 390×844px (iPhone 14 size) centered on desktop with phone-shaped border + shadow. Full-screen on actual mobile devices.

## Screens

### Splash Screen
- Auto-dismiss after 2 seconds
- App logo centered
- App name "ບໍ່ແກ້ວ Transit Pro" below logo
- Lao pattern animation (subtle pulse/fade)
- Green gradient background

### Screen 1: ໜ້າຫຼັກ (Home)

**Top section:**
- Welcome banner with gradient (green → dark green)
- App logo + "ບໍ່ແກ້ວ Transit Pro"
- Search bar: filters the route list below by matching origin or destination name. Typing "ປາກ" shows only routes with ປາກທາ. Empty search shows all routes.

**Service cards (2×2 grid):**
1. 🚕 ລົດ Taxi — tap goes to booking screen taxi section
2. 🚌 ປີ້ລົດເມ — tap goes to route list filtered by bus
3. 🚤 ປີ້ເຮືອ — tap goes to route list filtered by boat
4. 🗺️ ແຜນທີ່ — tap goes to map screen

**Routes section: ສາຍທາງຍອດນິຍົມ (Popular routes)**
Each route card shows:
- Route: origin → destination (e.g. ຫ້ວຍຊາຍ → ປາກທາ)
- Departure times (e.g. 08:00, 10:30, 14:00)
- Price in LAK (e.g. 50,000 ກີບ)
- Vehicle type icon (bus 🚌 or boat 🚤)
- "ຈອງ" (Book) button → goes to booking form with route pre-filled

### Screen 2: ຈອງ (Booking)

**Section A: ຈອງປີ້ (Book a Ticket)**
Form fields:
- ປະເພດ (Type): dropdown — ລົດເມ / ເຮືອ
- ຕົ້ນທາງ (From): dropdown of Bokeo stops
- ປາຍທາງ (To): dropdown of Bokeo stops
- ວັນທີ (Date): date picker
- ເວລາ (Time): dropdown filtered by selected route's available times from the routes table. If no route selected, shows placeholder "ເລືອກສາຍທາງກ່ອນ".
- ຈຳນວນບ່ອນນັ່ງ (Seats): number input (1-5)
- ລາຄາລວມ (Total price): route price × seat count. Updates live when either changes.
- Validation: From and To cannot be the same stop. All fields required. Show inline red text "ກະລຸນາເລືອກ" (Please select) for empty required fields on submit.
- Button: "ຢືນຢັນການຈອງ" (Confirm Booking)

After confirm: success overlay with:
- ✅ Green checkmark animation
- Booking ID (e.g. BKT-2026-001)
- QR code: 120×120px, generated inline as an SVG using a simple JS QR generator function (no library). Encodes the booking ID string. Black on white.
- Route + date + time summary
- "ເບິ່ງປີ້ຂອງຂ້ອຍ" (View my tickets) button

**Section B: ເອີ້ນ Taxi (Call Taxi)**
- ຈຸດຮັບ (Pick-up): text input with location icon
- ຈຸດສົ່ງ (Drop-off): text input with location icon
- ປະເພດລົດ (Car type): ທຳມະດາ (Standard) / VIP
- ລາຄາປະມານ (Est. price): auto-display
- Button: "ເອີ້ນ Taxi"
- After tap: animated status tracker:
  1. 🔍 ກຳລັງຊອກຫາຄົນຂັບ... (Searching for driver...)
  2. 🚗 ຄົນຂັບກຳລັງມາ (Driver on the way) — shows driver name + vehicle
  3. ✅ ຮອດແລ້ວ (Arrived)

### Screen 3: ແຜນທີ່ (Map)

- CSS-drawn simplified map of Bokeo province showing the Mekong river (blue curve along west/south border) and main road (green line inland). Styled with subtle terrain color (#E8F5E9 land, #BBDEFB river).
- Route lines: bus routes = green dashed on road, boat routes = blue solid on river
- Stop markers (gold circles with white text) at: ຫ້ວຍຊາຍ (northwest, on river), ຕົ້ນເຜິ້ງ (west, on river), ປາກທາ (south, on river), ຜາອຸດົມ (east, inland)
- Tap a marker → popup with stop name + next departure + price
- Legend at bottom explaining colors

### Screen 4: ໂປຣໄຟລ໌ (Profile)

**User info card:**
- Avatar (placeholder circle with initials)
- Name: ສົມໃຈ ວົງສະຫວັນ (demo name)
- Phone: 020 XX XXX XXX

**My tickets section: ປີ້ຂອງຂ້ອຍ**
List of booked tickets, each with:
- Route name
- Date + time
- Status badge:
  - 🟢 ຢືນຢັນແລ້ວ (Confirmed)
  - 🟡 ລໍຖ້າ (Pending)
  - 🔴 ຍົກເລີກ (Cancelled)
- Tap to expand: shows full details + QR code

**Menu items:**
- ປະຫວັດການເດີນທາງ (Travel history)
- ຕັ້ງຄ່າ (Settings)
- ກ່ຽວກັບ (About)
- ອອກຈາກລະບົບ (Logout)

## Navigation

**Bottom tab bar (fixed):** 4 tabs
1. ໜ້າຫຼັກ (Home) — house icon
2. ຈອງ (Book) — ticket icon
3. ແຜນທີ່ (Map) — map pin icon
4. ໂປຣໄຟລ໌ (Profile) — person icon

Active tab: green icon + green text + top indicator line
Inactive tab: gray icon + gray text

**Screen transitions:** Slide left animation (300ms ease) when navigating forward, slide right when going back.

**Splash → Home:** Fade out splash, fade in home (500ms).

## Fake Data

### Routes
| ID | From | To | Type | Times | Price (LAK) |
|----|------|----|------|-------|-------------|
| 1 | ຫ້ວຍຊາຍ | ຕົ້ນເຜິ້ງ | ລົດເມ | 07:00, 09:00, 13:00 | 30,000 |
| 2 | ຫ້ວຍຊາຍ | ປາກທາ | ລົດເມ | 08:00, 10:30, 14:00 | 50,000 |
| 3 | ຫ້ວຍຊາຍ | ຜາອຸດົມ | ລົດເມ | 06:30, 11:00 | 70,000 |
| 4 | ຫ້ວຍຊາຍ | ປາກທາ | ເຮືອ | 08:30, 14:00 | 80,000 |
| 5 | ຫ້ວຍຊາຍ | ຕົ້ນເຜິ້ງ | ເຮືອ | 09:00, 15:00 | 40,000 |

### Taxi
- Driver: ທ. ສົມພອນ, Toyota Vios ສີຂາວ, ທະບຽນ ບກ-1234
- Estimated prices: within ຫ້ວຍຊາຍ 20,000-40,000 ກີບ

### Profile
- Name: ສົມໃຈ ວົງສະຫວັນ
- Phone: 020 55 123 456
- 2 booked tickets (1 confirmed, 1 pending)

## File Structure

```
index.html          — single file with all HTML, CSS, JS
```

One file. Everything embedded. Open in browser to demo.
