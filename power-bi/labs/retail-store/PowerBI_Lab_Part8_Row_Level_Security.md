
# 🔐 Part 8: Row-Level Security (RLS) – Step-by-Step with Reasoning

---

### 🎯 Objective:
To restrict what users can see in your Power BI report based on their role (e.g., SalesRep, StockClerk, Manager). This ensures sensitive or irrelevant data is hidden from unauthorized viewers.

---

## ✅ Step 1: Add a New Table – `UserAccess`

Create a table to define what each user can access.

### Table Structure:
| Username           | Role        | ItemCode | Department  | Region   |
|-------------------|-------------|----------|-------------|----------|
| alice@abc.com     | SalesRep    | C01      | Sales       | North    |
| alice@abc.com     | SalesRep    | C03      | Sales       | North    |
| bob@abc.com       | Manager     | *        | Management  | All      |
| jane@abc.com      | StockClerk  | C02      | Warehouse   | East     |

> Load this table into Power BI and name it `UserAccess`.

---

## ✅ Step 2: Create Relationships

Link `UserAccess[ItemCode]` to each relevant data table:

| From Table     | To Table        | Column       |
|----------------|------------------|--------------|
| UserAccess     | Sales            | ItemCode     |
| UserAccess     | Inventory        | ItemCode     |
| UserAccess     | Purchases        | ItemCode     |
| UserAccess     | LeadTimeUpdates  | ItemCode     |
| UserAccess     | ConsumptionUpdates | ItemCode  |

Use single-direction filtering from `UserAccess`.

---

## ✅ Step 3: Define RLS in Power BI

1. Go to **Modeling > Manage Roles**
2. Create a new role: `RLS_Filter`
3. On `UserAccess`, use this DAX filter:

```DAX
UserAccess[Username] = USERNAME()
```

---

## ✅ Step 4: Handle Wildcard for Manager Role

If a user has `*` in `ItemCode`, they should see all items. Update your RLS like this:

```DAX
UserAccess[Username] = USERNAME() &&
(
    UserAccess[ItemCode] = "*" ||
    UserAccess[ItemCode] = RELATED(Sales[ItemCode])
)
```

Apply similar logic for other fact tables if needed.

---

## ✅ Step 5: Optional – Use a Central `ItemList` Table

To avoid many-to-many issues and simplify your model:
- Create `ItemList[ItemCode]`
- Link all fact tables and `UserAccess` to `ItemList`

This forms a star schema:  
`Sales → ItemList ← UserAccess`  
`Inventory → ItemList ← UserAccess`  
...

---

## ✅ Step 6: Test Your Roles

Use **Modeling > View As Roles** to simulate user access:
- alice@abc.com → should see only C01, C03
- jane@abc.com → should see only C02
- bob@abc.com → should see all items

---

## ✅ Step 7: Publish and Assign Roles

1. Publish to Power BI Service
2. Go to **Dataset > Security**
3. Assign user emails to the `RLS_Filter` role

---

## ✅ Summary

| Action                          | Purpose                                 |
|----------------------------------|-----------------------------------------|
| Add `UserAccess` Table          | Define who sees what                    |
| Create/Update Relationships     | Connect roles to fact tables            |
| DAX Role Filter                 | Match user login to permitted rows      |
| Wildcard Handling               | Allow managers to view everything       |
| Star Schema with `ItemList`     | Clean, scalable model structure         |
| View As Role                    | Simulate user-level experience          |

