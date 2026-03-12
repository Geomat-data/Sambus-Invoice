# Sambus Geospatial — Invoice Generator v2

## What's New in v2
- **Brand Colors**: Navy `#002e5a` + Green `#77B50C` extracted from sambusgeospatial.com
- **Invoice Valid / Terms & Cond**: Red text preserved at top right of invoice
- **Maintenance Years Logic**: When maint years > 0, total = unitPrice × qty × maintYrs
- **Markup**: Applied to BOTH displayed unit price and total (clients never see %)
- **Static Footer**: Footer banner always pinned to bottom of invoice page (never floats)

## How to Run
Simply open `index.html` in any modern browser.

Requires `prices.json` in the same folder for product search to work.

For best PDF output, use Chrome/Edge.

## Pricing Logic Summary
| Has Maint Years? | Unit Price Shown | Total Calculation |
|-----------------|-----------------|-------------------|
| No (maint=0)    | basePrice × (1+markup%) | unit × qty |
| Yes (maint>0)   | basePrice × (1+markup%) | unit × qty × maint |
