[Project3_README.md](https://github.com/user-attachments/files/28540362/Project3_README.md)
# Task3-Oluwabusola-Oyenuga# 🗄️ E-Commerce Sales — SQL Data Analysis
**DecodeLabs Data Analytics Internship | Project 3 | Batch 2026**

---

## 📌 Project Overview

This project uses SQL to extract meaningful insights from the e-commerce orders dataset. Using MySQL Workbench, 10 targeted queries were written to answer real business questions — going beyond surface-level metrics to uncover patterns that drive decisions.

---

## 🎯 Objective

- Write SQL queries to interrogate the dataset
- Use SELECT, WHERE, GROUP BY, ORDER BY, and aggregate functions
- Answer 10 specific business questions from the data
- Translate query results into actionable business insights

---

## 📁 File Structure

```
📂 DecodeLabs-Project-3/
│
├── 📄 ecommerce_queries.sql    # All 10 SQL queries
└── 📄 README.md                # Project documentation
```

---

## 📂 Dataset Summary

| Item | Value |
|---|---|
| Table Name | dataset |
| Total Records | 1,200 rows |
| Total Columns | 14 |
| Database | MySQL (decodelab schema) |
| Tool Used | MySQL Workbench |

---

## 🔎 Queries & Results

### Query 1 — Top Revenue Generating Product
```sql
SELECT product, ROUND(SUM(totalprice)) AS revenue
FROM dataset
GROUP BY product
ORDER BY revenue DESC
LIMIT 1;
```
**Result:** Chair — $195,620
**Insight:** Chair generates the highest total revenue of all 7 products.

---

### Query 2 — Average Order Value by Payment Method
```sql
SELECT PaymentMethod, SUM(totalprice) / COUNT(OrderID) AS AOV
FROM dataset
GROUP BY PaymentMethod
ORDER BY AOV;
```
**Result:** Credit Card leads at $1,127 | Debit Card lowest at $1,001
**Insight:** Credit card customers spend the most per order — a premium segment worth targeting.

---

### Query 3 — Cancelled vs Delivered vs Returned Orders
```sql
SELECT OrderStatus, COUNT(OrderID) AS orders
FROM dataset
WHERE OrderStatus IN ('Cancelled', 'Delivered', 'Returned')
GROUP BY OrderStatus
ORDER BY orders;
```
**Result:** Cancelled: 250 | Returned: 247 | Delivered: 231
**Insight:** Cancellations and returns outnumber delivered orders — a critical fulfilment problem.

---

### Query 4 — Referral Source by Total Spend
```sql
SELECT ReferralSource, SUM(TotalPrice) AS AmountSpend
FROM dataset
GROUP BY ReferralSource
ORDER BY AmountSpend;
```
**Result:** Instagram leads at $275,285 | Referral lowest at $226,815
**Insight:** Instagram is the highest-performing acquisition channel by total revenue generated.

---

### Query 5 — Monthly Revenue Trend
```sql
SELECT DATE_FORMAT(Date, '%Y-%m') AS Month,
       ROUND(SUM(TotalPrice), 2) AS Revenue
FROM dataset
GROUP BY Month
ORDER BY Month;
```
**Result:** 30 months of data (Jan 2023 – Jun 2025) | Peak: Jan 2023 at $56,685
**Insight:** Revenue is inconsistent month to month with no stable growth trend identified.

---

### Query 6 — Product with Highest Cancellations
```sql
SELECT Product, COUNT(OrderID) AS CancellationRate
FROM dataset
WHERE OrderStatus IN ('Cancelled')
GROUP BY Product
ORDER BY Product DESC
LIMIT 1;
```
**Result:** Tablet — 34 cancellations
**Insight:** Tablet leads in cancellations, suggesting a product listing or quality issue.

---

### Query 7 — Coupon vs Non-Coupon Spending
```sql
SELECT
  CASE WHEN CouponCode IS NULL OR CouponCode = 'N/A' THEN 'No Coupon'
       ELSE 'Used Coupon' END AS CouponUsage,
  COUNT(OrderID) AS Total_Orders,
  ROUND(AVG(TotalPrice), 2) AS Avg_Order_Value
FROM dataset
GROUP BY CouponUsage;
```
**Result:** Used Coupon: 891 orders ($1,057.64) | No Coupon: 309 orders ($1,043.37)
**Insight:** Coupon users spend $14 more on average — coupons attract higher-value buyers.

---

### Query 8 — Total Orders and Revenue per Product
```sql
SELECT Product,
       COUNT(OrderID) AS Total_Orders,
       ROUND(SUM(TotalPrice), 2) AS Revenue
FROM dataset
GROUP BY Product;
```
**Result:** All 7 products returned | Chair ($195,620) leads | Phone ($151,722) trails
**Insight:** Revenue is fairly distributed but Phone and Desk underperform relative to others.

---

### Query 9 — Average Order Value by Order Status
```sql
SELECT OrderStatus,
       ROUND(AVG(TotalPrice), 2) AS Avg_Order_Value
FROM dataset
GROUP BY OrderStatus
ORDER BY Avg_Order_Value DESC;
```
**Result:** Cancelled: $1,105.58 | Pending: $1,081.55 | Delivered: $1,050.22 | Returned: $984.93
**Insight:** Cancelled orders have the highest average order value — the business is losing its biggest spenders first.

---

### Query 10 — Top 5 Highest Value Orders
```sql
SELECT OrderID AS Orders,
       SUM(TotalPrice) AS Order_Value
FROM dataset
GROUP BY Orders
ORDER BY Order_Value DESC
LIMIT 5;
```
**Result:** ORD200789 leads at $3,456.40 | All top 5 above $3,370
**Insight:** Top orders are all bulk buyers — max quantity at high unit prices. A clear VIP segment.

---

## 💡 Key Insights Summary

| # | Insight |
|---|---|
| 1 | Only 19.3% of orders were successfully delivered |
| 2 | Cancelled orders have the HIGHEST average order value ($1,105) |
| 3 | Instagram drives the most revenue ($275,285) |
| 4 | Credit card users spend the most per order ($1,127) |
| 5 | Coupon users spend $14 more than non-coupon users |
| 6 | Tablet leads in cancellations — possible product issue |
| 7 | Top 5 orders are all bulk buyers — a VIP segment exists |
| 8 | Monthly revenue is inconsistent with no stable growth trend |

---

## ✅ Recommendations

| # | Recommendation |
|---|---|
| 1 | Investigate cancellations urgently — the business is losing its highest-value customers |
| 2 | Review Tablet product listing — high cancellation rate signals an expectation gap |
| 3 | Double down on Instagram marketing — highest revenue channel |
| 4 | Build a loyalty programme targeting credit card and bulk buyers |
| 5 | Expand coupon campaigns — data shows they attract higher-value buyers |
| 6 | Investigate monthly revenue dips to identify seasonal or operational patterns |

---

## 🛠️ Tools Used

- MySQL Workbench
- SQL (SELECT, WHERE, GROUP BY, ORDER BY, CASE WHEN, aggregate functions)

---

## 👩🏾‍💻 Analyst

**Oluwabusola Oyenuga**
Data Analyst | DecodeLabs Internship Batch 2026
[LinkedIn](https://www.linkedin.com/in/oluwabusola-oyenuga) | [GitHub](https://github.com/oluwabusola-may)
