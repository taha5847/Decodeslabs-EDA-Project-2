# 🔍 E-Commerce Orders: Exploratory Data Analysis (EDA)

> **Data Analytics Internship, Project 2 | DecodeLabs (Batch 2026)**
> Turning a raw table of 1,200 orders into clear, business-ready insights using Python.


## 📌 Project Overview

This project is an end-to-end **Exploratory Data Analysis** of an e-commerce order dataset. The goal is to understand patterns, trends and distributions in the data *before* any dashboarding or predictive modeling.

The analysis answers questions like:

- How are order values distributed, and where does the revenue actually come from?
- How do orders split across price tiers and quantity tiers?
- How has revenue moved over time?
- What share of orders are delivered, and what share are lost to cancellations and returns?
- Which numeric variables are related to each other?

## 🎯 Objectives

| Requirement | How it was addressed |
|---|---|
| Calculate basic statistics (mean, median, count) | `describe()`, `groupby()` aggregations, mode of segments |
| Identify trends and outliers | Yearly revenue trend, sorted `TotalPrice`, IQR check |
| Summarize key observations | See [Key Findings](#-key-findings) below |

## 📂 Dataset

**File:** `Dataset for Data Analytics.csv`  |  **Rows:** 1,200  |  **Columns:** 14  |  **Period:** Jan 2023 – Jun 2025

| Column | Description |
|---|---|
| `OrderID` | Unique order identifier |
| `Date` | Order date |
| `CustomerID` | Customer identifier (1,189 unique customers) |
| `Product` | Printer, Tablet, Chair, Laptop, Desk, Monitor, Phone |
| `Quantity` | Units ordered (1 to 5) |
| `UnitPrice` | Price per unit |
| `ShippingAddress` | Delivery address |
| `PaymentMethod` | Online, Cash, Credit Card, Debit Card, Gift Card |
| `OrderStatus` | Delivered, Shipped, Pending, Cancelled, Returned |
| `TrackingNumber` | Shipment tracking ID |
| `ItemsInCart` | Number of items in the cart (1 to 10) |
| `CouponCode` | SAVE10, WINTER15, FREESHIP or No Coupon |
| `ReferralSource` | Instagram, Email, Google, Facebook, Referral |
| `TotalPrice` | Order total (`Quantity × UnitPrice`) |

**Data quality check:** no missing values, no duplicate rows, no duplicate order IDs.

## 🛠️ Approach

1. **Load and inspect:** `head()`, `info()`, `describe()`
2. **Clean and convert:** convert `Date` to a proper datetime type
3. **Feature engineering:**
   - `PriceSegment`: **Low** (≤ 500), **Medium** (501 to 1,500), **High** (> 1,500)
   - `QuantitySegment`: **Low** (≤ 2), **Medium** (3 to 4), **High** (5)
   - `Year`: extracted from `Date`
4. **EDA:** grouped aggregations by `OrderStatus`, `PriceSegment` and `QuantitySegment`
5. **Visualization:** bar charts, line charts, pie chart and a correlation heatmap

## 📊 Key Findings

> All figures below were computed from the dataset in this repo.

**1. A small group of big orders drives most of the revenue**
High-value orders (the "High" segment, over 1,500) are only **26.8% of orders** but generate **56.1% of revenue** (~709.9K of ~1.26M). Low-value orders are 31.9% of orders but only **8.0%** of revenue.

**2. Order values are right-skewed**
The mean order value (**~1,054**) is well above the median (**~824**), with a skewness of about **0.89**. A handful of very large orders (8 flagged by the IQR rule) pull the average up, so the **median is the more honest "typical order"** figure.

**3. Over 40% of orders never complete**
**Cancelled (250) and Returned (247)** orders together make up **41.4% of all orders** and roughly **41% of total order value**. Only **231 orders (19.3%)** reached *Delivered* status. Cancelled orders are also the single largest status by value (~276K), mostly in the High segment (~165K).

**4. Revenue per month has softened since 2023**

| Year | Orders | Revenue | Avg. order value |
|---|---|---|---|
| 2023 | 510 | ~552.6K | ~1,084 |
| 2024 | 459 | ~480.2K | ~1,046 |
| 2025 (Jan–Jun only) | 231 | ~231.9K | ~1,004 |

⚠️ 2025 covers only six months, so compare **monthly pace**, not totals: about 46.1K/month in 2023, 40.0K/month in 2024 and 38.6K/month in 2025. Average order value has also drifted down each year.

**5. What moves the order total**
`TotalPrice` correlates most strongly with `UnitPrice` (**r ≈ 0.72**), then `Quantity` (**r ≈ 0.62**) and `ItemsInCart` (**r ≈ 0.39**). `Quantity` and `ItemsInCart` are also related (**r ≈ 0.65**), while `UnitPrice` is essentially independent of both.

**6. Quantity profile**
Medium-quantity orders (3 to 4 units) account for the most units sold (1,715 of 3,535), ahead of High (1,085) and Low (735).

## 💡 Business Takeaways

- **Protect the high-value tier.** It carries over half of revenue, so cancellations and returns inside it hurt the most.
- **Investigate the 41% cancel/return rate.** Even a small reduction here would recover more revenue than most acquisition campaigns.
- **Track the downward drift in average order value** and test bundling or threshold offers to lift it.

## 🧰 Tech Stack

- **Python 3**
- **Pandas** and **NumPy** for data manipulation
- **Matplotlib** and **Seaborn** for visualization
- **Jupyter Notebook**

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 3. Launch the notebook
jupyter notebook DecodeLabs.ipynb
```

> The notebook reads `Dataset for Data Analytics.csv` from the same folder. Keep the CSV next to the notebook (or update the filename in the first `read_csv` cell).

## 📁 Repository Structure

```
├── DecodeLabs.ipynb                # Full analysis notebook
├── Dataset for Data Analytics.csv  # Source dataset
└── README.md
```

## ⚠️ Limitations and Next Steps

- The dataset appears to be **synthetic**: order statuses, products, payment methods and referral sources are almost evenly distributed, so the status and channel splits may not reflect real customer behavior. Treat the *method* as the takeaway, not the exact business conclusions.
- `TotalPrice` equals `Quantity × UnitPrice` exactly, so **coupon discounts are not reflected** in the totals.
- Possible extensions: outlier handling with Z-score, monthly seasonality analysis, coupon and referral-source performance, and an interactive dashboard (Power BI / Tableau / Streamlit).

## 🙏 Acknowledgements

Completed as part of the **Data Analytics Internship, Project 2: Exploratory Data Analysis** at [DecodeLabs]

## 👤 Author



⭐ If you found this useful, consider giving the repo a star!
