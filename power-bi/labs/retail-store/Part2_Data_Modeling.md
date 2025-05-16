
# 🔗 Part 2: Data Modeling – Step-by-Step Guide

This part explains how to build relationships between tables in Power BI to create a functional data model for analysis.

---

## 🎯 Objective:
Establish proper relationships among the loaded tables to enable cross-table analysis and ensure accurate visuals.

---

## ✅ Step 1: Switch to Model View
- Click the **Model** icon (the third icon on the left sidebar that looks like a diagram).
- This will show all the loaded tables as blocks with their columns.

---

## ✅ Step 2: Understand Your Tables
Here’s a quick overview of what each table represents:

- **Sales**: Contains sales transactions with fields like `Date`, `ItemCode`, `Quantity`, `TotalPrice`.
- **Purchases**: Records purchases with fields such as `Date`, `ItemCode`, `Quantity`, `UnitPrice`.
- **Inventory**: The master table with static data like `ItemCode`, `ItemName`, and `StockLevel`.
- **LeadTimeUpdates**: Tracks lead time updates using `Date`, `ItemCode`, `EstimatedDays`, `ActualDays`.
- **ConsumptionUpdates**: Logs daily consumption by `Date`, `ItemCode`, `DailyConsumption`.

---

## ✅ Step 3: Create Relationships
We will now create **one-to-many** relationships based on the common field: `ItemCode`.

### 🔄 Relationship 1:
- Drag `ItemCode` from `Sales` and drop it onto `ItemCode` in `Inventory`.
- Set Cardinality: **Many to One**
- Cross Filter Direction: **Single**
- Click **OK**

### 🔄 Relationship 2:
- Drag `ItemCode` from `Purchases` to `Inventory[ItemCode]`
- Set Cardinality: **Many to One**
- Cross Filter Direction: **Single**
- Click **OK**

### 🔄 Relationship 3:
- Drag `ItemCode` from `LeadTimeUpdates` to `Inventory[ItemCode]`
- Cardinality: **Many to One**
- Click **OK**

### 🔄 Relationship 4:
- Drag `ItemCode` from `ConsumptionUpdates` to `Inventory[ItemCode]`
- Cardinality: **Many to One**
- Click **OK**

> 💡 Make sure `Inventory` acts as the central (lookup) table in your model.

---

## ✅ Step 4: Rename and Format Relationships (Optional)
- Double-click on any line (relationship) to rename it (e.g., “Sales ↔ Inventory”).
- This helps keep your model organized.

---

## ✅ Step 5: Validate the Model
- Ensure there are **no broken links** or **inactive relationships**.
- Every table should be connected through `ItemCode`.

---

## ✅ Step 6: Save Your Work
- Click **File > Save As**
- Save your Power BI project as:  
  `Sales_Inventory_Model.pbix`

---

You are now ready to build powerful visualizations based on this well-structured data model!
