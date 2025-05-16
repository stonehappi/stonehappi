
# 📊 Part 4: Data Visualization – Step-by-Step with Reasoning

### 🎯 Objective:
Use Power BI's visual tools to explore and present data effectively. This section will guide students to create insightful dashboards using different visual types that reflect business performance, inventory management, lead time reliability, and consumption trends.

---

## ✅ Step 1: Open Report View

**How:**  
Click the **Report View** icon (📊) on the left toolbar.

**Why:**  
This view provides a canvas to create visuals. All graphs and dashboards are built here.

---

## ✅ Step 2: Create Sales Trend Over Time

**Goal:** Visualize how sales have changed over time to spot trends or seasonality.

**How:**
1. Click on a blank space on the canvas.
2. In the **Visualizations** pane, click the **Line Chart** icon.
3. Drag `DateTable[Date]` to the **X-axis**.
4. Drag the DAX measure `Total Sales` to **Values**.
5. Rename title: **"Sales Trend Over Time"**
6. Format:
   - Turn on data labels.
   - Set X-axis as continuous.
   - Use Date hierarchy if needed.

**Why:**  
Line charts are perfect for showing changes over time. This helps stakeholders see if sales are increasing, steady, or dropping.

---

## ✅ Step 3: Show Inventory Levels by Item

**Goal:** Display how much stock is available for each item to detect understocking or overstocking.

**How:**
1. Choose **Clustered Bar Chart** from Visualizations.
2. Drag `Inventory[ItemName]` into **Axis**.
3. Drag `Inventory[StockLevel]` into **Values**.
4. Sort descending by StockLevel.
5. Title: **"Current Stock Level by Item"**

**Why:**  
Helps warehouse or supply chain teams understand which items are running low or are overstocked.

---

## ✅ Step 4: Compare Sales vs Purchases by Item

**Goal:** Identify if purchase quantity aligns with sales.

**How:**
1. Add a new **Stacked Column Chart**.
2. Drag `Inventory[ItemCode]` or `ItemName` to **Axis**.
3. Drag `Total Sales` to **Values**
4. Drag `Total Cost` from Purchases to **Values**
5. Rename: **"Sales vs Purchases Comparison"**
6. Add legend for distinction.

**Why:**  
See if the business is over-purchasing or under-purchasing relative to sales volume.

---

## ✅ Step 5: Analyze Lead Time Accuracy

**Goal:** Compare estimated vs actual lead time to assess supplier reliability.

**How:**
1. Add **Line Chart**.
2. Axis: `DateTable[Date]`
3. Values: `EstimatedDays`, `ActualDays`
4. Title: **"Lead Time Accuracy Over Time"**

**Why:**  
Helps analyze logistics performance and supplier dependability.

---

## ✅ Step 6: Visualize Daily Consumption Pattern

**Goal:** Monitor daily usage of items.

**How:**
1. Insert **Area Chart**.
2. X-axis: `DateTable[Date]`
3. Values: `DailyConsumption`
4. Legend: `ItemName`
5. Title: **"Daily Consumption Trend"**

**Why:**  
Reveals which items are in high demand and when — helpful for forecasting.

---

## ✅ Step 7: Add Slicers for Interactivity

**Goal:** Let users filter data by time or item.

**How:**
1. Insert **Slicer** visual.
2. Add:
   - `Year`
   - `Month`
   - `ItemName`
   - `Stock Status` (from DAX)

**Why:**  
Slicers let users control views without changing the actual report design.

---

## ✅ Step 8: Display KPIs Using Cards

**Goal:** Highlight important metrics.

**How:**
1. Use **Card** visuals for:
   - `Total Sales`
   - `Sales YTD`
   - `Average Daily Sales`
   - `Average Lead Time Difference`

**Why:**  
KPI cards provide at-a-glance performance indicators.

---

## ✅ Step 9: Layout and Dashboard Design Tips

**How:**
- Group visuals:
  - Top: KPIs & Slicers
  - Middle: Sales & Inventory
  - Bottom: Lead Time & Consumption
- Use consistent colors and alignment.

**Why:**  
Clear, organized dashboards make it easier for decision-makers to understand insights.

---

## ✅ Step 10: Save Your Report

**How:**  
File > Save As > `Sales_Inventory_Visualization.pbix`

**Why:**  
To preserve work, share with others, or publish to Power BI Service.
