# E-Commerce Sales, Profitability & Customer Analytics Dashboard

## Overview

This project is an interactive Power BI dashboard built to analyze an e-commerce business from different angles — sales, profitability, products, customers, regions, and shipping operations.

I used the Superstore e-commerce dataset containing **51,290 transaction records**. The project follows an end-to-end analytics workflow, starting with data cleaning and transformation and ending with an interactive dashboard and business recommendations.

The main objective was to go beyond simply showing sales numbers and understand **where the business is performing well, where profitability can be improved, and which areas may need attention.**

---

## Business Questions

The dashboard was designed to answer questions such as:

- Which categories and sub-categories generate the most sales and profit?
- Which products contribute most to overall sales?
- Which customer segment is the most valuable?
- Which regions perform best in terms of sales and profit?
- Where are there signs of weaker profitability?
- How do discount levels relate to profit?
- Which shipping modes are used most frequently?
- Which shipping modes have longer delivery times?
- Which regions have higher shipping costs?

---

## Tools & Technologies

- **Power BI**
- **Power Query**
- **DAX**
- **Excel / CSV**
- **Star Schema Data Modeling**

---

## Dataset

The project uses a Superstore e-commerce dataset with:

- **51,290 rows**
- **27 original columns**

The data contains information about orders, customers, products, sales, profit, discounts, regions, markets, shipping modes, shipping costs, and dates.

Some of the main fields include:

`Order.ID`, `Order.Date`, `Customer.ID`, `Customer.Name`, `Product.ID`, `Product.Name`, `Category`, `Sub.Category`, `Sales`, `Profit`, `Quantity`, `Discount`, `Region`, `Segment`, `Ship.Mode`, `Ship.Date`, and `Shipping.Cost`.

---

## Data Preparation

I used **Power Query** to prepare the dataset before building the dashboard.

The main steps included:

- Reviewed the dataset structure and column types
- Checked the data for missing values
- Removed the `记录数` field because it contained only one distinct value and did not provide analytical value
- Created a `Delivery Days` column using Order Date and Ship Date
- Prepared separate customer and product dimensions
- Prepared a dedicated date table for time-based analysis
- Organized the model into fact and dimension tables

The final model follows a **star schema** with:

```text
                 DimDate
                    |
                    |
DimCustomer ---- FactSales ---- DimProduct
```

This structure keeps the model organized and makes the analysis easier to maintain.

---

## Data Model

### Fact Table

**FactSales**

Contains the transaction-level sales data and measures such as:

- Sales
- Profit
- Quantity
- Discount
- Shipping Cost
- Delivery Days
- Order ID
- Customer ID
- Product ID
- Order Date

### Dimension Tables

**DimDate**
- Date
- Year
- Quarter
- Month
- Year Month

**DimCustomer**
- Customer ID
- Customer Name
- Segment
- City
- State
- Country
- Region
- Market
- Market2

**DimProduct**
- Product ID
- Product Name
- Category
- Sub-Category

---

## Key DAX Measures

Some of the main measures used in the dashboard are:

```DAX
Total Sales = SUM(FactSales[Sales])
```

```DAX
Total Profit = SUM(FactSales[Profit])
```

```DAX
Total Quantity = SUM(FactSales[Quantity])
```

```DAX
Total Orders = DISTINCTCOUNT(FactSales[Order.ID])
```

```DAX
Total Customers = DISTINCTCOUNT(FactSales[Customer.ID])
```

```DAX
Profit Margin % =
DIVIDE([Total Profit], [Total Sales], 0)
```

```DAX
Average Order Value =
DIVIDE([Total Sales], [Total Orders], 0)
```

```DAX
Average Delivery Days =
AVERAGE(FactSales[Delivery Days])
```

These measures were used to create dynamic KPIs and charts that respond to the selected filters.

---

## Dashboard Pages

The dashboard contains five pages.

### 1. Executive Overview

Provides a high-level view of the business through:

- Total Sales
- Total Profit
- Profit Margin
- Total Orders
- Total Customers
- Average Order Value
- Sales and Profit trend
- Category performance
- Regional performance

### 2. Sales & Product Performance

Focuses on product and sales performance through:

- Sales by Sub-Category
- Top 10 Products by Sales
- Sales vs Profit by Product
- Sales, Quantity, Orders and AOV KPIs

### 3. Profitability Analysis

Focuses on understanding profit and margin:

- Profit by Sub-Category
- Sales vs Profit
- Discount vs Profit
- Total Profit
- Profit Margin
- Total Sales

### 4. Customer & Regional Analysis

Analyzes customer segments and regional performance:

- Sales by Segment
- Profit by Segment
- Sales by Region
- Customer, Sales and Profit KPIs

### 5. Shipping & Operations

Looks at operational performance:

- Orders by Ship Mode
- Average Delivery Days by Ship Mode
- Shipping Cost by Region
- Total Orders
- Average Delivery Days
- Total Shipping Cost

All pages include interactive slicers relevant to the analysis.

---

## Key Findings

### Technology was the strongest category

Technology generated approximately **4.75M in sales** and **664K in profit**, making it the strongest category based on both sales and profitability.

### Furniture showed a profitability opportunity

Furniture generated approximately **4.11M in sales**, but its profit was only around **285K**.

This indicates that high sales volume does not necessarily mean strong profitability and makes Furniture an area worth investigating further.

### Smartphones were prominent among top-selling products

Several smartphone products appeared among the highest-selling products, including products from Apple, Cisco, Motorola, and Nokia.

This suggests that smartphone products are important contributors to overall sales.

### Consumer was the strongest customer segment

Consumer customers generated the highest sales and profit among the three segments.

Approximate profit contribution:

- Consumer: **650K**
- Corporate: **382K**
- Home Office: **231K**

### Regional performance varied

Central was the highest-sales region in the dashboard, while several other regions contributed considerably less.

This highlights the importance of looking at regional performance separately rather than treating all regions in the same way.

### Standard Class dominated shipping volume

Standard Class accounted for approximately **15.2K orders**, making it the most frequently used shipping mode.

It also had the highest average delivery time at approximately **5 days**.

### Discount and profitability need to be monitored

The Discount vs Profit analysis shows differences in profitability at different discount levels.

This analysis indicates areas that deserve further investigation, but it does not prove that discounting directly causes lower profit.

---

## Business Recommendations

Based on the analysis:

1. **Review Furniture profitability** by examining product-level margins, pricing, and discount levels.
2. **Continue monitoring Technology products** because the category is currently the strongest contributor to sales and profit.
3. **Focus on the Consumer segment** through retention and targeted customer strategies.
4. **Investigate regional differences** to understand why some regions perform better than others.
5. **Review shipping strategy**, especially Standard Class, to balance delivery time and shipping cost.
6. **Use discounts carefully** and evaluate their impact on profit rather than focusing only on sales growth.

---

## Project Workflow

```text
Raw E-Commerce Data
        ↓
Data Cleaning & Transformation
        ↓
Power Query
        ↓
Star Schema Data Model
        ↓
DAX Measures
        ↓
Business Analysis
        ↓
Interactive Power BI Dashboard
        ↓
Business Insights & Recommendations
```

---

## Project Files

```text
ecommerce-sales-profitability-powerbi/
│
├── README.md
├── insights.md
│
├── data/
│   └── superstore.csv
│
├── powerbi/
│   └── ECommerce_Sales_Profitability.pbix
│
└── screenshots/
    ├── executive-overview.png
    ├── sales-product-performance.png
    ├── profitability-analysis.png
    ├── customer-regional-analysis.png
    └── shipping-operations.png
```

---

## What I Learned

Through this project, I practiced the complete Power BI workflow rather than focusing only on visualization.

The main areas I worked on were:

- Data cleaning with Power Query
- Data modeling and relationships
- Star schema design
- Date table creation
- DAX measures
- Filter context and interactive analysis
- KPI development
- Choosing appropriate visualizations
- Business-oriented analysis
- Converting analysis into actionable insights

---

## Conclusion

This project helped me understand how a Data Analyst can take raw transactional data and turn it into a useful business reporting solution.

The dashboard brings sales, profitability, customer, regional, and operational information into one place, while the accompanying analysis highlights areas that can support better business decisions.

The most important takeaway from the project is that **sales alone do not tell the complete story**. Looking at profit, customers, regions, discounts, and operations together gives a much clearer picture of business performance.
