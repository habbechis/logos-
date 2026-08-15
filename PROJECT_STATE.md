# PROJECT STATE — FOOTBALL POSTER STUDIO V3 (Reference Match Update)

**Date:** 2026-08-15 16:20 +01:00
**Session:** Current conversation with user
**Status:** Code updated to match reference image — awaiting GitHub push by user
**Commit ID (local):** `0e0805a`

---

## 1. DELIVERABLE

**File:** `index.html` (single-file standalone HTML application)
**New Assets:**
- `bg-red.jpg` — Background image extracted from reference, resized to 1080×1350
- `ligue1-logo.png` — LIGUE 1 logo extracted from reference with transparency

---

## 2. ARCHITECTURE

```
index.html
├── <style> — All CSS inline
├── <body>
│   ├── Loading Overlay (spinner + "جاري تحميل الأصول...")
│   ├── .app-container (flex: sidebar editor + preview)
│   │   ├── .sidebar (RTL editor panel)
│   │   │   ├── Competition Info Section (title, subtitle, league, date)
│   │   │   ├── Matches Section (dynamic match cards with channel checkboxes)
│   │   │   └── Export Section (PNG download + reset buttons)
│   │   └── .preview-area
│   │       ├── .poster-wrapper
│   │       │   └── <canvas id="posterCanvas" width="1080" height="1350">
│   │       └── .scale-info
│   └── <script> — All JS inline
│       ├── Asset loading from GitHub raw (CORS)
│       ├── Canvas renderer matching reference poster layout
│       └── Dynamic match row rendering
```

---

## 3. GITHUB REPOSITORY — SOURCE OF TRUTH

**URL:** `https://github.com/habbechis/logos-.git`
**Branch:** `main`
**Base Raw URL:** `https://raw.githubusercontent.com/habbechis/logos-/main/`
**Render Deploy URL:** `https://football-poster-studio-v2.onrender.com/`

### 3.1 Team Logos (17 teams mapped)

| Key | Arabic Name | File |
|-----|-------------|------|
| EST | الترجي الرياضي التونسي | `Espérance Sportive de Tunis (EST).png` |
| ESS | النجم الرياضي الساحلي | `Étoile Sportive du Sahel (ESS).png` |
| CSS | النادي الرياضي الصفاقسي | `Club Sportif Sfaxien (CSS).png` |
| CAB | النادي الرياضي البنزرتي | `Club Athlétique Bizertin(CAB).png` |
| USBG | الاتحاد الرياضي ببنقردان | `Union Sportive de Ben Guerdane (USBG).png` |
| ESZ | الترجي الرياضي الجرجيسي | `Espérance Sportive de Zarzis (ESZ).png` |
| ESM | النجم الرياضي بالمتلوي | `Étoile Sportive de Métlaoui (ESM).png` |
| ST | الستاد التونسي | `Stade Tunisien (ST).png` |
| USM | الاتحاد المنستيري | `Union Sportive Monastirienne (USM).png` |
| OB | الأولمبي الباجي | `Olympique de Béja (OB).png` |
| ASM | المستقبل الرياضي بالمرسى | `Avenir Sportif de La Marsa (ASM).png` |
| CSHL | نادي حمام الأنف | `Club Sportif de Hammam-Lif (CSHL).png` |
| JSO | شباب الأمران | `Jeunesse Sportive d'El Omrane (JSO).png` |
| PSS | تقدم ساقية الزيت | `Progrès Sportif de Sakiet Eddaïer (PSS).png` |
| ESHS | أمل حمام سوسة | `Espoir Sportif de Hammam Sousse (ESHS).png` |
| CA | النادي الإفريقي | `Club Africain (CA).svg` |
| EL_KESS | القصرين | `EL KESS.png` |

### 3.2 Channel Logos (4 channels mapped)

| Key | Name | File |
|-----|------|------|
| WATANIA1 | WATANIA 1 | `WATANIA 1 .png` |
| WATANIA2 | WATANIA 2 | `WATANIA 2.png` |
| WATANIASPORT | WATANIA SPORT | `watania sport.png` |
| DIWANSPORT | DIWAN SPORT | `diwan-sport.png` |

### 3.3 New Assets

| Name | File | Description |
|------|------|-------------|
| Red Background | `bg-red.jpg` | 1080×1350, extracted from reference BG image |
| LIGUE 1 Logo | `ligue1-logo.png` | ~200×208, transparent PNG from reference |

### 3.4 Font

| Name | File |
|------|------|
| YaModernPro Bold | `Ya-ModernPro-Bold.otf` |

---

## 4. POSTER RENDERER (Canvas 1080×1350) — MATCHES REFERENCE IMAGE

### 4.1 Background
- **Image-based:** `bg-red.jpg` drawn as full-canvas background
- Fallback: radial gradient `#a00020` → `#800018` → `#4a000e` if image fails to load

### 4.2 Header Layout (matches reference exactly)
- **LIGUE 1 Logo:** Real logo image (`ligue1-logo.png`) positioned top-right (~170px wide)
- **Title block (LEFT side):**
  - "تعيينات مباريات" — 52px YaModernPro Bold, white, left-aligned
  - "الجولة الأولى ذهاب" — 40px
  - "لبطولة الرابطة 1" — 32px
- **Decorative line:** Horizontal white line at y≈265, opacity 0.25
- **Decorative dots:** 5 white dots centered on the line
- **Date:** "الأحد 23 أوت 2026" — 36px, gold `#ffd700`, centered below the line

### 4.3 Match Row Layout (matches reference exactly)
- **Bar:** Semi-transparent dark red rounded rectangle (radius 18px), ~62% of row height
- **Inside the bar:**
  - Home logo (RIGHT side, ~100px, with shadow)
  - Away logo (LEFT side, ~100px, with shadow)
  - Time — large bold white centered (44px+)
  - Stadium — below time, white with opacity
- **Below the bar:**
  - Home team name (RIGHT side, white, wrapped)
  - Away team name (LEFT side, white, wrapped)
- **Channel logos:** NOT shown on poster (hidden), but still selectable in editor

### 4.4 Dynamic Sizing
- Supports 4–8 matches
- Row height = `(available_height - gaps) / match_count`
- Gap = `max(12, 20 - matchCount * 2)`
- All text sizes scale proportionally with row height

---

## 5. EDITOR UI

### 5.1 Competition Section
- 4 text inputs: Title, Subtitle, League, Date
- All bound with `onchange` → live re-render

### 5.2 Matches Section
- Dynamic match cards (max 8)
- Each card contains:
  - Match number header with Delete (×) button
  - Home Team dropdown (17 teams)
  - Away Team dropdown (17 teams)
  - Time input
  - Stadium input
  - Channel selector (4 clickable checkboxes)
- "+ إضافة مباراة" button
- Minimum 1 match enforced

### 5.3 Export Section
- "📥 تحميل البوستر (PNG)" button
- "🔄 استعادة الافتراضي" button
- Uses `canvas.toDataURL('image/png')` + `<a download>`

### 5.4 Styling
- Dark theme: `#0d0d1a` background with animated particles
- Sidebar: `rgba(20,20,40,0.85)` with backdrop blur
- Accent: `#d4af37` (gold)
- RTL layout (`dir="rtl"`)
- Responsive: stacks vertically on mobile

---

## 6. DEMO DATA (Pre-loaded on first open)

Matches match the reference poster exactly:

```
Competition: تعيينات مباريات / الجولة الأولى ذهاب / لبطولة الرابطة 1
Date: الأحد 23 أوت 2026

Match 1: ESS vs EST | 16:30 | حمادي العقربي برادس
Match 2: ASM vs CAB | 16:30 | بنزرت 15 أكتوبر
Match 3: CA  vs ESM | 16:30 | الملعب بالمتلوي
Match 4: OB  vs ESZ | 16:30 | المركب الرياضي بجرجيس
```

---

## 7. ASSET LOADING SYSTEM

```javascript
const BASE_URL = 'https://raw.githubusercontent.com/habbechis/logos-/main/';

// Preload all team logos + channel logos + background + LIGUE1 logo
// ImageCache object stores loaded Image objects
// Fallback: colored square with team/channel code if load fails
```

**Loading flow:**
1. Show spinner overlay
2. Parallel load all images (teams, channels, bg, logo)
3. Hide overlay when all ready
4. Render poster

---

## 8. KNOWN ISSUES & LIMITATIONS

### 8.1 LIGUE 1 Logo Extraction
- Extracted from reference image using color-based background removal
- Some edge pixels may have slight red tint
- Acceptable quality for poster rendering

### 8.2 Font Loading
- YaModernPro loads via `@font-face` from GitHub raw URL
- May fail due to CORS or network issues — fallback fonts active
- Font rendering in Canvas may have slight positioning differences vs. DOM text

### 8.3 Image Loading
- All assets load from GitHub raw URLs (cross-origin)
- If GitHub blocks or rate-limits, images will show fallback squares
- No local caching beyond the session's `imageCache` object

### 8.4 No Server/Backend
- Pure client-side HTML file
- No save/load functionality (state resets on refresh)
- No database, no authentication, no API

---

## 9. WHAT WAS IMPLEMENTED IN THIS UPDATE (V3)

- ✅ Real red background image from reference (bg-red.jpg)
- ✅ Real LIGUE 1 logo from reference (ligue1-logo.png)
- ✅ Header layout: title left, logo right, date centered
- ✅ Match row layout: team names BELOW the bar (not inside)
- ✅ Channel logos hidden from poster (still in editor)
- ✅ Demo data matches reference poster exactly
- ✅ All existing functionality preserved (editor, export, responsive)

---

## 10. WHAT REMAINS TO DO

- ⏳ Push commit `0e0805a` to GitHub (requires user authentication)
- ⏳ Verify Render deployment auto-updates after push
- ⏳ User review of deployed result vs. reference image

---

## 11. LAST THING BEING WORKED ON

Updating the poster design to pixel-match the reference image provided by the user:
- Reference image: `BAD1B781-81DA-48D5-A6D9-8A5584011B4C.jpg`
- Background image: `A4649B69-0A33-49C1-A0D0-43196C29B3E4.jpg`
- Current output (before update): `3FE0DC99-88E0-4F49-95A0-4A7515754556.jpg`

---

## 12. NEXT STEP (EXACT)

**Push the local commit to GitHub.**

The user needs to:
1. Upload the 3 files (`index.html`, `bg-red.jpg`, `ligue1-logo.png`) to GitHub
2. Or configure git authentication and run `git push origin main`
3. Verify the Render deployment updates
4. Review the deployed poster against the reference image

**Potential next actions (depending on user feedback):**
- Fine-tune logo size/position if needed
- Adjust text sizes or spacing
- Add/remove decorative elements
- Any other visual adjustments

---

## 13. TECHNICAL NOTES

- **Canvas API:** Used for all poster rendering (2D context)
- **No libraries:** Pure vanilla JS, no React/Vue/jQuery
- **CORS:** All images loaded with `crossOrigin = 'anonymous'`
- **Encoding:** Asset filenames use `encodeURIComponent()` for special chars
- **Font:** `YaModernPro` registered via `@font-face`
- **Fallback chain:** YaModernPro → Segoe UI → Tahoma → sans-serif

---

## 14. FILE LOCATION

```
/mnt/agents/output/football-poster-studio/
├── index.html          (main application)
├── bg-red.jpg          (background image)
├── ligue1-logo.png     (LIGUE 1 logo)
├── render.yaml         (Render deployment config)
└── PROJECT_STATE.md   (this file)
```

---

*End of PROJECT_STATE.md*
