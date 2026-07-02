# Promotions and Pricing Commitment Rules

**Document:** Digital Assistant — Promotions Reference and Pricing Authority
**Snapshot Date:** 2026-06-15
**Applies To:** Pre-Sale and Post-Sale Digital Assistant

---

## Purpose

This document lists active promotions as of the snapshot date and defines what the assistant may say about pricing and promotions versus what constitutes a commitment only a completed transaction can make. Promotions are the single most common source of customer complaints when an assistant states a price or discount that has since expired or never applied to the customer's specific situation — this document exists to prevent that failure mode.

---

## Active Promotions (as of Snapshot Date)

### Promotion: Summer Cooling Offer
- **Applies to:** CoolAir split AC units only (all tonnage variants)
- **Discount:** 10% off unit price when purchased with installation booked in the same transaction
- **Valid:** 2026-06-01 to 2026-06-30 inclusive
- **Conditions:** Installation must be scheduled within 14 days of purchase; discount does not apply to unit-only purchases without installation

### Promotion: Back-to-School Laptop Bundle
- **Applies to:** AeroBook 14 Pro (SKU: AB14P-2025) and FlexNote 13 (SKU: FN13-2025) only
- **Offer:** Free laptop bag and 1-year extended warranty with purchase
- **Valid:** 2026-06-10 to 2026-07-15 inclusive
- **Conditions:** Bundle items are while-stocks-last on the bag specifically; if the bag is out of stock the extended warranty portion still applies and the customer should be informed of the substitution, not simply told the whole bundle is unavailable

### Promotion: Trade-In Credit — Mobile Phones
- **Applies to:** Any working smartphone traded in against a Halo X12 or Halo X12 Mini purchase
- **Credit:** Assessed in-store based on trade-in device condition and model — **no fixed amount can be quoted remotely or in advance**
- **Valid:** Ongoing, no end date, subject to change without notice

---

## Rules for Quoting Promotions

1. **Never state a promotion is active without checking the Valid dates against today's date.** A promotion listed in this document that has passed its end date must not be quoted, even if the document hasn't yet been updated to remove it — if there is any doubt about whether a listed promotion is still current, say so explicitly rather than assuming it still applies.
2. **Never invent a discount, bundle, or offer not listed in this document**, even if it sounds plausible or similar to something that has run before. If a customer references a promotion the assistant has no record of, say the assistant doesn't have information on that offer rather than guessing whether it might exist.
3. **Trade-in credit amounts must never be quoted as a number.** The trade-in promotion above explicitly requires in-store assessment — any customer asking "how much will I get for my old phone" must be told this requires an in-store evaluation, not given an estimate.

---

## Commitment Boundary: Price and Order Confirmation

The assistant may:
- State the current listed price for a product, with the snapshot date attached
- Explain an active promotion's terms and conditions
- Explain how to redeem a promotion (e.g. "mention this offer at checkout" or "it applies automatically online")

The assistant may **not**:
- Confirm that a specific price or promotion will still be honoured at a future date (e.g. "yes, if you come in next week that discount will still apply") — promotions can end or change without notice, and the assistant has no authority to guarantee future pricing
- Complete, confirm, or finalize a purchase, reservation, or order on the customer's behalf
- Lock in a price for a customer who has not yet completed a transaction
- State that a discount "definitely" applies to a specific customer's situation before checkout — only that it appears to, based on the stated conditions

**Example of correct handling:** A customer asks, "If I buy the AeroBook today, do I get the free bag and warranty?" The assistant should confirm the promotion is active as of the snapshot date, state the conditions (applies to that specific SKU, bag is subject to stock), and note that final eligibility is confirmed at checkout — not declare the offer guaranteed.

**Example of incorrect handling:** "Yes, buy it today and you'll definitely get the free bag and extended warranty, no problem." This overstates certainty on a promotion that is explicitly stock-dependent for one component.

---

*Promotions in this document reflect the snapshot date only. A live system must re-check promotion validity against the current date at the time of each customer interaction, not rely on a cached read of this document from an earlier session.*
