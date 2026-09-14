# Retail Margin and Pricing Optimisation

Analysis of Australian retail sales data to identify which product categories are driving margin, which are dragging it, and where pricing adjustments would have the highest impact on profitability.

---

## The Business Problem

A mid-size Australian retailer has a profitability problem but does not know where it is coming from. They have sales data across multiple product categories and four regions but cannot answer three critical questions:

1. Which categories are actually making money and which are quietly losing it?
2. Is discounting helping or hurting? Are they giving away margin on products that would have sold anyway?
3. Where should they adjust pricing to improve profitability without losing sales volume?

---

## The Dataset

**Source:** Kaggle Superstore Sales Dataset, synthetic but built on realistic retail transaction structure with sales, profit, discount, quantity, and product category columns.

No publicly available Australian retail dataset includes cost, margin, and discount columns together, so this dataset was reframed as an Australian retailer by replacing the US geography with Australia, NSW, VIC, QLD and WA; removing city and postcode fields that were not needed for category-level analysis; and converting USD values to AUD at 1.55.

**Derived columns added:**

- Cost = Sales - Profit
- Margin % = (Profit / Sales) x 100
- Revenue without discount = Sales / (1 - Discount)
- Discount Loss = Revenue without discount - Sales
- Year and Quarter extracted from Order Date for time-series analysis

**Key data decision:** Median sales ($83.56 AUD) was used as the segmentation threshold rather than mean ($353.75 AUD). A small number of very large transactions were pulling the mean up significantly and would have misrepresented where the midpoint of the business actually sits.

---

## Python Analysis

**Data cleaning**

Before any analysis the dataset was cleaned by converting dates to datetime format, stripping whitespace from text columns, removing duplicates, converting categorical columns to category dtype, and validating that derived columns were calculated consistently.

**Quadrant segmentation**

All 12 category-region combinations were plotted on a scatter chart with total sales on the x-axis and total profit on the y-axis. Two reference lines divided the chart into four quadrants:

- Vertical line at median total sales separating high and low volume
- Horizontal line at zero profit separating profitable from loss-making

Zero was chosen as the profit threshold rather than median profit because the question is whether a combination is making or losing money, not whether it is above or below average.

Quadrant labels: Invest (high sales, positive profit), Grow (low sales, positive profit), Fix (high sales, negative profit), Review (low sales, negative profit).

**Margin waterfall**

A waterfall chart was built for each category to separate cost structure problems from discounting problems. It shows four components in sequence: revenue without discount, discount loss, cost, and actual profit. The consolidated results are reported in Key Findings below.

---

## SQL Analysis

All SQL was run inside the Jupyter notebook using SQLite via SQLAlchemy. The cleaned pandas dataframe was loaded into a SQLite database and queried directly to keep the entire workflow in one notebook.

**Margin and profit by region, category, and quarter**

Is that margin holding up over time, or is a strong headline number hiding a declining trend by quarter?

```sql
SELECT
    Region,
    Category,
    Year,
    Quarter,
    SUM(Profit) AS total_profit,
    SUM(Sales) AS total_sales,
    ROUND((SUM(Profit) / SUM(Sales)) * 100, 2) AS weighted_margin
FROM superstore
GROUP BY Region, Category, Year, Quarter
ORDER BY Year, Quarter, Region, Category;
```

**Profit by exact discount level**

At what discount level does profit turn negative for each category-region combination?

```sql
SELECT
    Category,
    Region,
    Discount AS discount_level,
    COUNT(*) AS total_transactions,
    ROUND(AVG(Profit), 2) AS avg_profit_per_transaction,
    ROUND(SUM(Profit), 2) AS total_profit
FROM superstore
GROUP BY Category, Region, Discount
ORDER BY Category, Region, Discount;
```

Additional queries covering discount frequency, average discount, and volume comparison are in the notebook.

---

## Tableau Dashboards

Two dashboards were built for different audiences.

**CFO Summary Dashboard:** For executive decision-making. Shows total profit, total sales, average margin, profit by region and category, and quarterly profit trends. Region and Category filters update all visuals simultaneously.

**Commercial Deep Dive Dashboard:** For commercial managers. Shows quadrant segmentation, weighted margin vs average discount, profit threshold by discount level, and revenue lost to discounting by segment. Includes a KPI showing +0.04 units volume difference to address the sales team objection directly.

[View CFO Summary Dashboard](https://public.tableau.com/app/profile/delia.colaco/viz/AustralianRetailMarginDiscountAnalysisCFOSummary/CFOSummary)

[View Commercial Deep Dive Dashboard](https://public.tableau.com/app/profile/delia.colaco/viz/AustralianRetailMarginDiscountAnalysis/CommercialMarginDiscountAnalysisAustralianRetail?publish=yes)

---

## Key Findings

- VIC Furniture is the only loss-making segment (-1.70% weighted margin), driven by cost rather than discounting: cost consumes 97% of revenue, and even eliminating all discounts would only recover $291,791, not enough to fix the segment without supplier renegotiation.
- 67.84% of VIC Furniture transactions are discounted at an average depth of 29.74%
- Profit turns negative for VIC Furniture between 20% and 30% discount
- The VIC Office Supplies 80% discount tier alone costs $47,376 in total profit loss
- Discounting above 30% increases units sold by only +0.04 per transaction on average
- WA Technology and NSW Office Supplies are the strongest performing combinations

---

## Files in This Repo

| File | What it is |
|---|---|
| `Superstore Sales Dataset.ipynb` | Full analysis notebook |
| `quadrant-segmentation.png` | Python quadrant segmentation chart |
| `margin-waterfall-furniture.png` | Margin waterfall for Furniture |
| `margin-waterfall-office-supplies.png` | Margin waterfall for Office Supplies |
| `margin-waterfall-technology.png` | Margin waterfall for Technology |

---

## Tools Used

Python, Pandas, Matplotlib, Seaborn, SQLAlchemy, SQL, SQLite, Tableau Public
