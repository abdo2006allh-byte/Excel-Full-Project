# MISUO — Furniture Sales & Delivery Dashboard

This project is an Excel-based order management system for a furniture brand called **MISUO** (beds, sofas, tables, etc.). It contains raw customer order data along with an interactive **Pivot Table dashboard** (with slicers and charts) to track sales performance and delivery operations.

---

## 📁 File Structure

The workbook contains 3 sheets:

| Sheet | Description |
|---|---|
| `البيانات` (Data) | Raw order-level table (113 real orders, 24 columns) — customer, product, price, delivery, status... |
| `Pivot` | The dashboard: multiple pivot tables + 5 charts + a slicer to filter by product |
| `Sheet1` | Mostly empty helper sheet (leftover slicer elements) |

---

## 🧾 Key Columns

| Column | Content |
|---|---|
| Customer Name / trimmed | Customer name, with a manually added "trimmed" (whitespace-cleaned) version |
| Customer Type | Individual / Company |
| Governorate / Address | Customer location |
| Sales Platform | Order source (Homzmart, Chic Homes, Oscar Rutten, Facebook, referral...) |
| Product Name / Design / Type / Size / Metal Color / Fabric Color / Description | Product specifications |
| Selling Price / Quantity / Deposit | Order financial values |
| Payment Method | Prepaid / cash on delivery / company account... |
| Order Date / Due Delivery Date / Actual Delivery Date | Order lifecycle dates |
| Delivery Performance | on time / late / cancelled |
| Customer Waiting Days | Gap between the agreed and actual delivery date |
| Delivery Owner | Shipping company or a named delivery agent |
| Status | Delivered / Returned |

---

## 📊 Data Analysis — Key Numbers

- **Real order count:** 113 orders (the sheet's formal range extends to row 252, but rows 114–252 are completely empty).
- **Time period:** Orders from July 27, 2024 to December 14, 2024 (~4.5 months of activity).
- **Total order value:** ≈ 1,144,690, of which ≈ 904,571 corresponds to orders actually marked "Delivered."
- **Average selling price:** ≈ 10,220, ranging from 4,020 to 21,999 — high-value furniture items.
- **Unique customers:** 76 across 113 orders, meaning a notable share of repeat customers.
- **Customer type split:** 80 individual orders vs. 33 company orders.
- **Best-selling product:** Beds ("سرير") dominate with 75 orders, followed by sofas (18) and tables (17).
- **Top sales channel:** "Homzmart" alone accounts for roughly 62% of orders, followed by "Chic Homes" and "Oscar Rutten."
- **Delivery status:** 91 orders "Delivered" vs. 22 "Returned" → a **return rate of ≈ 19.5%**, which is notably high and worth investigating.
- **Delivery performance (completed orders only):** 58 "late" vs. 33 "on time" — **over 60% of completed deliveries were late**, a clear operational weak point.
- **Delivery ownership:** the vast majority of deliveries are handled by a single person, with the rest via a shipping company — a concentration risk (single point of failure).
- **Colors:** Black is the most requested metal color (43 orders), followed by white (30); fabric color data is largely missing since it doesn't apply to all products.

---

## 📈 Dashboard Analysis (Pivot Sheet)

The dashboard is built from ~9 pivot tables, 5 charts, and one slicer (filtering by Product Name), covering:

1. **Total Orders** — order count by delivery status.
2. **Average Selling Price**.
3. **Sales by Platform** — revenue split by sales channel.
4. **Best Seller** — top product by quantity.
5. **Best Color Sold**.
6. **On-Time Delivery Rate** — on time / late / cancelled.
7. **Delivery Status Breakdown** — delivered vs. returned.
8. **Orders by Area** — geographic distribution by governorate.
9. **Number of Companies / Number of Persons**.
10. **Total Sales** — delivered vs. returned value.
11. **Sales Over the Year** — monthly sales trend.

> ⚠️ **Note:** All these tables are linked to a slicer on the "Product Name" field. The values currently cached in the file reflect the last saved filter state (in this case, only 8 orders), not necessarily the full dataset. When opening the file, run **Refresh All** on the pivot tables and make sure the slicer is set to "Select All" before reading any figure.

---

## 🧹 Data Cleaning Findings

- **Empty trailing rows:** the sheet formally extends to row 252, but real data ends at row 113; rows 114–252 are empty.
- **One corrupted row (129):** contains a `#VALUE!` formula error and a raw Excel date serial number, isolated from the rest of the data — should be deleted.
- **Leading/trailing whitespace** is the biggest data quality issue, causing single categories to be split into duplicates in the pivot tables — e.g., `"محمود على"` vs `"محمود على "`, `"مسبق الدفع"` vs `"مسبق الدفع "`, `"دورين"` vs `"دورين "`, and similar cases across governorate, design, and type columns. Even column headers themselves contain trailing spaces (e.g., `"سعر البيع "`).
- **Inconsistent spelling** of the same category in a few cases (e.g., `"فانتستيك"` vs `"فانتاستك"`).
- **Missing values:** some are structural/expected (e.g., fabric color only applies to certain products), while others (15 rows) correspond to near-empty trailing rows within the 113-row range and should be reviewed.

**Recommended cleaning steps:** remove empty/corrupted rows → trim whitespace across all text columns and headers → standardize inconsistent category spellings → add data validation to the "Delivery Performance" column → refresh all pivot tables with the slicer set to "Select All" → document that missing product-spec values mean "not applicable," not "missing."

---

## 💡 Key Operational Insights

- **Late deliveries are the most visible problem**: over 60% of completed orders were delivered late.
- **The ~19.5% return rate** is high for furniture at this price point and warrants deeper investigation (correlation with lateness, platform, or product?).
- **Heavy reliance on a single sales platform and a single delivery person** represents a concentration risk in both the sales channel and operations.
- **Beds dominate sales**, raising the question of whether other products are under-marketed or genuinely lower in demand.

---

## 🛠️ Tools Used
Microsoft Excel — Pivot Tables, Pivot Charts, Slicers.

