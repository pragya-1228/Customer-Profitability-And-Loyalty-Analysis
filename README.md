# 📈 Customer Profitability & Loyalty Analysis (Q2–Q3 2025)

## 🎯 Project Overview

This project documents a **Customer Profitability and Loyalty Analysis** conducted on transactional sales data from **April to September 2025**.

The primary goal was to quantify customer value using key metrics (**LTV**, **AOV**, **Repeat Rate**) and segment the business's product offerings into actionable categories (**Food**, **Vet**, **Grooming**) to drive targeted marketing and operational strategies.

---

## 💾 Data Source & Environment

* **Source File:** `dwarka raw data.xlsx - Sheet1.csv`
* **Time Period:** 6 months (April 2025 – September 2025)
* **Tools Used:** Microsoft Excel (Initial Calculation), Power BI (Dashboard & DAX Modeling)

---

## 📊 Core Key Performance Indicators (KPIs)

| KPI                               | Definition                                                    | Final Value   | Business Implication                                        |
| :-------------------------------- | :------------------------------------------------------------ | :------------ | :---------------------------------------------------------- |
| **Customer Lifetime Value (LTV)** | Average total revenue expected from a single unique customer. | **₹4,778.81** | Sets the maximum limit for Customer Acquisition Cost (CAC). |
| **Average Order Value (AOV)**     | Average revenue generated per transaction/order.              | **₹637.13**   | Measures transaction size and success of upselling.         |
| **Customer Repeat Rate**          | % of unique customers who made 2+ purchases.                  | **77.89%**    | Excellent indicator of loyalty and satisfaction.            |

---

## 💡 Strategic Insights by Macro Category

All metrics were grouped into three macro-categories: **Food**, **Grooming**, and **Vet**.

| Macro Category | Total Revenue | AOV         | LTV        | Repeat Rate | Key Insight                                                                 |
| :------------- | :------------ | :---------- | :--------- | :---------- | :-------------------------------------------------------------------------- |
| **Food**       | ₹4.36 Million | ₹636.97     | **₹3,390** | **66.87%**  | **The Loyalty Engine.** Highest revenue and retention.                      |
| **Grooming**   | ₹2.03 Million | **₹960.93** | ₹2,324     | 48.45%      | **High-Value Transaction.** Highest per-visit spend, but lower repeat rate. |
| **Vet**        | ₹1.53 Million | ₹604.37     | ₹2,184     | 60.23%      | **Strong Retainer.** Indicates customer trust in health services.           |

---

## 📈 Advanced Analysis: AOV Trend

| Month      | AOV Trend          | Insight                                                 |
| :--------- | :----------------- | :------------------------------------------------------ |
| **August** | **₹720.31 (Peak)** | Highest customer spend — investigate promotions or mix. |
| **June**   | **₹567.14 (Low)**  | Lowest spend — analyze causes for mid-year dip.         |

---

## 🛠️ Technical Methodology (DAX Measures)

### **1. Total Sales, Transactions, and Customer Count**

```dax
Total Sales = SUM('Sales'[Sales Amount])

Total Transactions = COUNTROWS('Sales')

Total Unique Customers = DISTINCTCOUNT('Sales'[Customer Name])

AOV = DIVIDE([Total Sales], [Total Transactions], 0)

LTV = DIVIDE([Total Sales], [Total Unique Customers], 0)
```

---

### **2. Customer Loyalty Measures (Repeat Rate)**

This logic identifies and counts unique customers who placed more than one order.

```dax
Repeat Customer Count =
VAR CustomerTransactionCount =
    ADDCOLUMNS(
        VALUES('Sales'[Customer Name]),
        "TransactionCount", CALCULATE(COUNTROWS('Sales'))
    )
RETURN
    COUNTROWS(
        FILTER(
            CustomerTransactionCount,
            [TransactionCount] > 1
        )
    )

Repeat Rate = DIVIDE([Repeat Customer Count], [Total Unique Customers], 0)
```

---

### **3. RFM Segmentation (Conceptual Logic)**

RFM (Recency, Frequency, Monetary) analysis was used to classify customers for targeted marketing.

```dax
RFM Segment =
SWITCH(TRUE(),
    'RFM Table'[R_Score] >= 4 && 'RFM Table'[F_Score] >= 4 && 'RFM Table'[M_Score] >= 4, "Champions (Highest Value)",
    'RFM Table'[R_Score] <= 2 && 'RFM Table'[F_Score] >= 3 && 'RFM Table'[M_Score] >= 3, "Can't Lose Them (Urgent Win-Back)",
    'RFM Table'[R_Score] >= 4 && 'RFM Table'[F_Score] = 1, "New Customers (Nurture)",
    "Other Segments"
)
```

---

## 🚀 Key Business Recommendations

1. **Increase AOV with Bundles** – Implement cross-selling strategies pairing high-AOV services (Grooming, Vet) with high-margin accessories to lift AOV above ₹637.
2. **Protect the Loyalty Engine** – Ensure 100% stock for high-repeat items (Food, Medicine). Any shortage risks customer churn and loyalty erosion.
3. **Launch a VIP Program** – Use RFM segmentation to reward Top 50 “Champion” customers with exclusive offers to retain high-LTV segments.
4. **Seasonality Watch** – Investigate the August peak to replicate success and mitigate June’s dip.

---

**🧩 Result:**
This project demonstrates a full-cycle customer analytics workflow — from cleaning and modeling sales data to generating actionable business strategies through Power BI and DAX.
