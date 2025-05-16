
# 🧮 Part 3: Using DAX to Perfect the Model  
### *(Calculated Columns, Measures, Date Intelligence, and Advanced DAX)*

---

### 🎯 Objective:
This section introduces DAX (Data Analysis Expressions) to enrich your data model. You'll learn to:
- Add custom calculations using DAX.
- Use date intelligence for time-based comparisons.
- Build more flexible and insightful reports.

---

## 📌 What is DAX?

**DAX** stands for **Data Analysis Expressions**. It is a formula language used to:
- **Create Calculated Columns** → Adds new columns to tables row by row.
- **Create Measures** → Returns a single value based on aggregation logic (SUM, AVERAGE, etc.).
- **Create Calculated Tables** → Like a query that returns a whole table.

DAX is similar to Excel formulas but is optimized for data models and visual analysis.

---

## ✅ Step 1: Create Calculated Columns (Row-by-Row Logic)

### 🔹 Add `TotalPrice` to Sales Table
```DAX
TotalPrice = Sales[Quantity] * Sales[UnitPrice]
```
**Explanation:** Multiplies each row’s quantity by its unit price to compute revenue per sale.

---

### 🔹 Add `TotalCost` to Purchases Table
```DAX
TotalCost = Purchases[Quantity] * Purchases[UnitPrice]
```
**Explanation:** This tells you the cost of inventory purchased per transaction.

---

## ✅ Step 2: Create Simple Measures (Aggregated Logic)

### 🔹 Total Sales
```DAX
Total Sales = SUM(Sales[TotalPrice])
```
**Explanation:** Sums the `TotalPrice` column from the `Sales` table across all rows.

---

### 🔹 Average Lead Time Difference
```DAX
Average Lead Time Diff = AVERAGE(LeadTimeUpdates[ActualDays] - LeadTimeUpdates[EstimatedDays])
```
**Explanation:** Shows whether actual delivery is generally faster or slower than the estimate.

---

## ✅ Step 3: Create a Central Date Table

### 🔹 Why a Date Table?
- Enables **YTD, MTD, YoY** analysis
- Power BI can’t perform time intelligence without a proper date table

### 🔹 Create Date Table
```DAX
DateTable = 
ADDCOLUMNS (
    CALENDAR (DATE(2020,1,1), DATE(2025,12,31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Quarter", "Q" & FORMAT([Date], "Q"),
    "Weekday", FORMAT([Date], "dddd")
)
```

### 🔹 Mark as Date Table
- Select the table
- Click **Modeling > Mark as Date Table**
- Choose the `[Date]` column

### 🔹 Create Relationships
- Link `DateTable[Date]` to:
  - `Sales[Date]`
  - `Purchases[Date]`
  - `LeadTimeUpdates[Date]`
  - `ConsumptionUpdates[Date]`

---

## ✅ Step 4: Time Intelligence Measures

### 🔹 Sales Year-to-Date (YTD)
```DAX
Sales YTD = TOTALYTD(SUM(Sales[TotalPrice]), DateTable[Date])
```

### 🔹 Sales Month-to-Date (MTD)
```DAX
Sales MTD = TOTALMTD(SUM(Sales[TotalPrice]), DateTable[Date])
```

### 🔹 Sales Previous Month
```DAX
Sales Prev Month = 
CALCULATE(
    SUM(Sales[TotalPrice]),
    PREVIOUSMONTH(DateTable[Date])
)
```

### 🔹 Year-over-Year (YoY) Growth
```DAX
Sales YoY Growth = 
VAR ThisYear = CALCULATE(SUM(Sales[TotalPrice]), YEAR(DateTable[Date]) = YEAR(TODAY()))
VAR LastYear = CALCULATE(SUM(Sales[TotalPrice]), YEAR(DateTable[Date]) = YEAR(TODAY()) - 1)
RETURN DIVIDE(ThisYear - LastYear, LastYear)
```

---

## ✅ Step 5: Advanced DAX for Business Insights

### 🔹 Percentage of Total Sales (All Items)
```DAX
% of Total Sales = 
DIVIDE(
    SUM(Sales[TotalPrice]),
    CALCULATE(SUM(Sales[TotalPrice]), ALL(Sales))
)
```

### 🔹 Sales Rank by Item
```DAX
Sales Rank = 
RANKX(
    ALL(Inventory[ItemName]),
    CALCULATE(SUM(Sales[TotalPrice])),
    ,
    DESC
)
```

### 🔹 Average Daily Sales
```DAX
Avg Daily Sales = 
DIVIDE(
    SUM(Sales[TotalPrice]),
    DISTINCTCOUNT(Sales[Date])
)
```

### 🔹 Stock Status Alert
```DAX
Stock Status = IF(Inventory[StockLevel] < 50, "Low", "OK")
```

---

## 🧠 Summary

| DAX Type             | Use Case                              | Benefit                                |
|----------------------|----------------------------------------|----------------------------------------|
| Calculated Column    | Row-by-row data prep                   | Enhances raw data                      |
| Measure              | Aggregated KPIs                        | Drives visuals and summaries           |
| Time Intelligence    | YTD, MTD, PrevMonth, YoY               | Enables time-based decision making     |
| Advanced DAX         | % of total, ranking, conditionals      | Adds depth and logic to your reports   |
