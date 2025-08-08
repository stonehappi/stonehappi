# 🧪 Part 1: Data Loading – Step-by-Step Guide

This section teaches students how to **import Excel data into Power BI** properly. Follow these instructions carefully.

---

## ✅ Step 1: Open Power BI Desktop
- Double-click the Power BI Desktop icon on your computer.
- Wait for the interface to fully load.

---

## ✅ Step 2: Get Data from Excel
- On the **Home** tab, click the **Get Data** dropdown.
- Choose **Excel Workbook** from the list.

---

## ✅ Step 3: Browse and Select the File
- Locate and select the file named:  
  `SmartSimulated_2020_2025.xlsx`
- Click **Open**.

---

## ✅ Step 4: Navigator Window
- A window will appear listing all the sheets in the Excel file.
- You will see the following available sheets:
  - `Sales`
  - `Purchases`
  - `Inventory`
  - `LeadTimeUpdates`
  - `ConsumptionUpdates`
  - `NewTableName` <!-- Add the actual new table name here -->

> ✅ **Tip:** Click each sheet once to preview the data on the right side.

---

## ✅ Step 5: Select Sheets to Load
- Check the boxes next to the following sheets:
  - ✔️ Sales
  - ✔️ Purchases
  - ✔️ Inventory
  - ✔️ LeadTimeUpdates
  - ✔️ ConsumptionUpdates
  - ✔️ NewTableName <!-- Add the actual new table name here -->
- Click the **Load** button (bottom right corner).

> ⚠️ Do **not** click "Transform Data" yet — we’ll do that in Part 2 if cleaning is needed.

---

## ✅ Step 6: Wait for Loading
- Power BI will now import the selected tables.
- You’ll see a **Fields pane** appear on the right side of Power BI with all your loaded tables and their columns.

---

## ✅ Step 7: Verify Data Tables
- Confirm that the tables appear in the **Data** view:
  - Click the **Data** icon (table symbol) on the left sidebar.
  - Browse through each table to verify:
    - `Sales`: Date, ItemCode, Quantity, TotalPrice, etc.
    - `Purchases`: Date, ItemCode, Quantity, UnitPrice, etc.
    - `Inventory`: ItemCode, ItemName, StockLevel, etc.
    - `LeadTimeUpdates`: Date, ItemCode, EstimatedDays, ActualDays
    - `ConsumptionUpdates`: Date, ItemCode, DailyConsumption
    - `NewTableName`: ... <!-- Add a brief description of columns for the new table -->
