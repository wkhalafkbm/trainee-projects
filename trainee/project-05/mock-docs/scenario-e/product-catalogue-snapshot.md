# Product Catalogue Snapshot

**Document:** Digital Assistant — Product Data Reference
**Snapshot Date:** 2026-06-15
**Data Source:** Merchandising System export, refreshed daily at 02:00 Kuwait time
**Applies To:** Pre-Sale and Post-Sale Digital Assistant

---

## Purpose and Freshness Notice

**This is a snapshot, not a live feed.** Every answer the assistant gives about stock, price, or specifications must be understood as accurate only as of the Snapshot Date above. The real catalogue changes daily — new stock arrives, prices change, and products are discontinued. Any system built against this document must:

1. Attach the data's snapshot date or last-refresh timestamp to every answer involving stock, price, or a time-limited spec
2. Treat any product or price not present in the current data export as unknown, not as "unavailable" or "discontinued" — the assistant should say it doesn't have current information rather than guessing
3. Never state a specification, price, or stock level with confidence if the underlying data is missing or ambiguous

A trainee building against this document should design as if this file will be regenerated daily with different contents — the assistant's behaviour should not depend on memorising the specific numbers below.

---

## Category: Laptops

### Product: AeroBook 14 Pro (SKU: AB14P-2025)
- **Price:** KWD 349.000
- **Stock:** 23 units — Salmiya, Avenues, Marina Mall branches; online fulfilment available
- **Specs:** 14" 1920x1200 display, 16GB RAM, 512GB SSD, 11-hour battery life (manufacturer rated)
- **Compatibility note:** Charges via USB-C (65W); does not include a charger in the box as of this batch — sold separately (SKU: CHG-65W-USBC)

### Product: AeroBook 14 Pro (Previous Batch, SKU: AB14P-2024)
- **Price:** KWD 289.000 (clearance — while stock lasts)
- **Stock:** 4 units — Avenues branch only
- **Specs:** Same as AB14P-2025 except 8-hour battery life (manufacturer rated) and includes a 45W charger in the box
- **Note:** This is a different SKU from the current AB14P-2025 despite the identical product name. The assistant must distinguish these by SKU, not by name alone, when answering stock or battery-life questions — a customer asking "does the AeroBook 14 Pro come with a charger" needs to be asked which batch/SKU before an accurate answer can be given.

### Product: FlexNote 13 (SKU: FN13-2025)
- **Price:** KWD 219.000
- **Stock:** 0 units at all branches — next restock estimated 2026-07-01 (estimate only, not guaranteed)
- **Specs:** 13.3" 1920x1080 display, 8GB RAM, 256GB SSD, 9-hour battery life

---

## Category: Mobile Phones

### Product: Halo X12 (SKU: HX12-128)
- **Price:** KWD 279.000 (128GB variant)
- **Stock:** 61 units across all branches
- **Specs:** 6.5" OLED display, 128GB storage, dual SIM, IP68 water resistance

### Product: Halo X12 (SKU: HX12-256)
- **Price:** KWD 329.000 (256GB variant)
- **Stock:** 14 units — Avenues and Marina Mall only
- **Specs:** Identical to HX12-128 except 256GB storage

### Product: Halo X12 Mini (SKU: HX12M-128)
- **Price:** KWD 219.000
- **Stock:** 38 units across all branches
- **Specs:** 6.1" OLED display, 128GB storage, dual SIM, IP67 water resistance (lower rating than the standard X12 — this is a genuine spec difference, not a typo)

---

## Category: Home Appliances

### Product: CoolAir 1.5-Ton Split AC (SKU: CA15T-INV)
- **Price:** KWD 165.000 (unit only, installation charged separately per `returns-and-repair-policy.md` service rates)
- **Stock:** 47 units in central warehouse; branch stock varies — confirm branch-level availability before promising same-day pickup
- **Specs:** Inverter type, 1.5-ton cooling capacity, energy rating A++

---

## Discontinued / Removed From Catalogue

The following products are no longer sold and must not be quoted as available under any circumstances, even if a customer references an old advertisement or receipt: **AeroBook 12 Air (SKU: AB12A-2023)**, **Halo X10 (all variants)**. If a customer asks about these for a warranty or repair matter (not a purchase), route to `returns-and-repair-policy.md` — post-sale support continues for discontinued products still within their warranty period even though they can no longer be purchased.

---

*This snapshot expires at the next daily refresh. Any answer generated from this document should be treated as stale after 24 hours and should not be cached or reused across days without confirming a newer snapshot is not available.*
