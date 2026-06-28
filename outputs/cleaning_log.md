# Cleaning Log — Part 1: Business Data Cleaning
**Dataset:** raw_orders.xlsx  
**Analyst:** Radha Manasa Peesapati 
**Date:** June 2026

---

## Issues Found

**Text Fields**  
Inconsistent casing, leading/trailing spaces, and extra internal spaces were found across all categorical columns. PROPER and TRIM were applied to standardise all 9 text columns.

**Dates**  
Four mixed date formats were found in order_date and ship_date. All dates were converted to a consistent datetime format. Slash-format dates were interpreted as MM/DD/YYYY based on data pattern — no first component exceeded 12 across 319 dates. 21 records had ship_date earlier than order_date and were flagged.

**Duplicates**  
20 exact duplicate rows were removed. 12 order IDs appeared with conflicting information (different status/sales values) — these 24 rows were flagged for manual review and retained.

**Discounts**  
- 18 missing → treated as 0 (all other sales fields valid)
- 15 negative → flagged as invalid
- 8 stored as text percentages → converted to decimal, flagged as above range
- 2 above 0.55 → flagged as invalid

**Missing Values**  
region (25 rows) and ship_mode (21 rows) filled as "Unknown".

**Sales Mismatches**  
25 rows had sales values inconsistent with quantity × unit_price × (1 - discount). A calculated_sales column was created; original sales column retained.

---

## Business Rules Applied

- Cancelled orders and failed payments excluded from completed sales summary via pivot filters
- Returned/refunded orders summarised separately
- Ship before order date → flagged, records retained
- Negative and out-of-range discounts → flagged, not corrected
- Missing discounts → treated as 0 where all other sales fields valid

---

## Assumptions

- Slash dates treated as MM/DD/YYYY based on data evidence
- Max valid discount set at 0.55 based on dataset distribution
- "Unknown" retained as category in pivot summaries

---

## Limitations

- 14 missing-discount rows have sales inconsistent with zero discount — actual values unknown
- Conflicting duplicates could not be resolved without source system access
- Sales mismatches retained pending further investigation

---

## Record Summary

| Category | Count |
|---|---|
| Original records | 932 |
| Duplicates removed | 20 |
| Final record count | 912 |
| Clean | 785 |
| Warning | 59 |
| Invalid | 68 |
| Flagged for review | 24 |

