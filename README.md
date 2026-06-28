# Part 1: Business Data Cleaning, Validation & Excel Reporting

## Assignment Overview
This part involves cleaning and validating a raw retail orders dataset exported from multiple internal systems. The cleaned data is used to create summary reports for business review.


## Dataset
**File:** raw_orders.xlsx  
**Records:** 932 (original), 912 (after cleaning)  
**Columns:** 21 (original), 35 (after calculated columns added)

The dataset contains order-level sales data including customer details, product information, shipping, discounts, and payment status.


## Tools Used
- Microsoft Excel (cleaning, validation, pivot tables)


## Cleaning Steps Performed

1. **Text standardisation** — TRIM and PROPER applied to 9 categorical columns to fix casing and spacing issues
2. **Date standardisation** — Four mixed date formats converted to a consistent datetime format; 21 invalid ship dates flagged
3. **Duplicate handling** — 20 exact duplicate rows removed; 24 conflicting duplicate rows flagged for review
4. **Missing values** — region and ship_mode filled as "Unknown"; missing discounts treated as 0
5. **Discount validation** — Negative discounts and out-of-range values flagged; text percentages converted to decimal
6. **Calculated columns** — cleaned_discount, calculated_sales, calculated_profit, profit_margin, shipping_delay_days, order_month, order_year, data_quality_flag added


## Business Rules Applied

- Cancelled orders and failed payments excluded from completed sales summary
- Returned/refunded orders summarised separately
- Ship dates before order dates flagged as invalid records
- Missing discounts treated as 0 where all other sales fields were valid
- Negative and above-range discounts flagged, not corrected


## Data Quality Issues Found

| Issue | Count |
|---|---|
| Missing region | 25 |
| Missing ship_mode | 21 |
| Missing discount | 18 |
| Exact duplicate rows | 20 |
| Conflicting duplicate order IDs | 12 (24 rows) |
| Negative discounts | 15 |
| Invalid date format / ship before order | 21 |
| Sales calculation mismatches | 25 |


## Pivot Reports Summary

| Report | Key Finding |
|---|---|
| Sales by Region | South has highest sales; East has highest profit margin (30.70%) |
| Sales by Category | Furniture and Technology nearly equal in total sales |
| Orders by Ship Mode | Standard Class most used (242 orders); Same Day least (204) |
| Profit Margin by Segment | Small Business highest margin (28.98%); overall margin ~28.86% |
| Cancelled/Returned/Failed by Region | North has most cancellations (48); South highest failed payments (20) |
| Monthly Sales Trend | Sales consistent across months; Nov–Dec 2025 data not yet available |


## Key Business Insights

- Overall profit margin is approximately 28.67% across all regions
- East region has the highest profit margin despite not having the highest sales
- Standard Class is the dominant shipping mode, accounting for 26.5% of all orders
- 308 orders were either cancelled or returned — about 34% of total orders, which is worth investigating
- Sales are relatively stable month-on-month with no strong seasonal spike observed


## Assumptions and Limitations

- Slash-format dates treated as MM/DD/YYYY based on data pattern evidence
- Maximum valid discount assumed to be 0.55 based on dataset distribution
- 14 missing-discount rows may have had actual discounts applied — could not be confirmed
- Conflicting duplicate records retained and flagged; could not be resolved without source system access


## Screenshots

| File | Description |
|---|---|
| raw_data_preview.png | Raw dataset before cleaning |
| cleaned_data_preview.png | Cleaned dataset with all calculated columns |
| pivot_summary_1.png | Sales and profit by region |
| pivot_summary_2.png | Monthly sales trend by year |

