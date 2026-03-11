# Sambus Geospatial — Invoice Generator
**Version 2.0 · March 2026**

A fully offline, browser-based Proforma Invoice system for Sambus Geospatial Nigeria Limited.

---

## Quick Start
1. Open `index.html` in any modern browser (Chrome, Edge, Firefox)
2. No installation, no server, no internet required after first load
3. Google Fonts (Inter) load from CDN on first use — works offline with system fonts as fallback

---

## Features

### Invoice Creation
- **Document Types**: Proforma Invoice, Quotation, Commercial Invoice, Tax Invoice
- **Auto PFI numbering** — sequential invoice numbers stored in browser
- **Live preview** — both pages update as you type
- **2-page PDF export** — Page 1 (invoice) + Page 2 (T&C)

### Products & Pricing
- **2,354 products** across all categories loaded from `prices.json`
- **Categories**: Server, Single Use, Named User, Concurrent License, Admin/NPO/EDU,
  ESRI Partner Network, Training, PS, ENVI, Trimble, Wingtra
- **Searchable dropdowns** — type any part of a product name
- **Maintenance Years** column per line item
- **Duplicate line** button (⧉) to copy a line item instantly
- **Per-line markup %** — silently applied, never shown to client

### Currency Support
| Button | Shows on invoice |
|--------|-----------------|
| ₦ Naira (NGN) | Prices in NGN + USD equivalent footnote |
| $ USD | Prices in USD + NGN equivalent footnote |
| ₵ Cedis (GHS) | Prices in GHS + USD equivalent footnote |
| 🌐 All | USD / NGN / GHS on every line |

- Set FX rates manually (USD→NGN, USD→GHS)
- VAT % configurable (default 7.5%)
- Discount % at invoice level

### Sales Team Management
- Add/edit/delete salespersons with name, title, email, phone
- Upload signature image (PNG/JPG) — embeds on invoice footer
- All salesperson data stored in browser localStorage

### Bank Details
- NGN account details section
- Optional FCY/USD account section (shown only if filled)

### Draft Management
- **💾 Save Draft** — saves current invoice to browser localStorage
- **📂 Load Draft** — restores last saved draft
- **✕ New** — resets form, increments PFI sequence

---

## Updating Prices
When Esri or other vendors release new pricing:

1. Export the new price sheet to CSV/Excel
2. Run the extraction script (see `update_prices.py` if included, or re-run the original Python extraction)
3. Replace `prices.json` in this folder
4. Reload the browser — all 2,354+ products reflect new prices immediately
5. **Nothing else changes** — no formulas to fix, no helper sheets to update

The `prices.json` format is:
```json
[
  {
    "id": "160458",
    "name": "ArcGIS Enterprise Advanced Up to Four Cores Perpetual License",
    "basePrice": 69300.00,
    "category": "Server"
  }
]
```

---

## Markup Logic
Markup is applied per line item: `Total = UnitPrice × Qty × (1 + Markup%/100)`

- Set **category-level defaults** in Settings tab (e.g. Server=20%, PS=30%)
- Override per line item in the Products tab
- Markup % is **never printed** on the invoice PDF

---

## Files
| File | Purpose |
|------|---------|
| `index.html` | The entire app (single file, ~150KB) |
| `prices.json` | 2,354 product price records |
| `README.md` | This file |

---

## Browser Storage
All settings, salesperson data, and drafts are stored in `localStorage` — they persist
across browser sessions on the same computer. To clear: open DevTools → Application →
Local Storage → clear entries starting with `sg_`.

---

## Technical Notes
- **PDF generation**: html2canvas 1.4.1 + jsPDF 2.5.1 (loaded from CDN)
- **Font**: Inter (Google Fonts CDN), fallback to system-ui
- **No backend required** — 100% client-side
- **Print support**: Ctrl+P hides the UI, prints invoice pages only
