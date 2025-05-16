
# 📈 Part 9: Report Enhancements for Row-Level Security (RLS)

---

### 🎯 Objective:
To align your Power BI report design with your RLS model so users only see what they’re authorized to see, while ensuring the report remains informative and user-friendly.

---

## ✅ 1. Add a “Current User” Card

**How:**
1. Create a measure:
```DAX
CurrentUser = USERNAME()
```
2. Add a **Card** visual and use this measure.

**Why:**  
Confirms that RLS is being applied and identifies the currently logged-in user.

---

## ✅ 2. Display the User’s Role (Optional)

**How:**
1. Create a measure:
```DAX
UserRole = 
CALCULATE(
  VALUES(UserAccess[Role]),
  UserAccess[Username] = USERNAME()
)
```
2. Show this value using a **Card** or **Table** visual.

**Why:**  
Lets the user (and you during testing) know which role they're assigned.

---

## ✅ 3. Review Visual Filters

**Action:**
- Ensure all visuals use `ItemCode` (or relevant) filtering from the RLS model.
- Use **View as Role** to test role-level results.

**Why:**  
Protects against unauthorized data exposure and ensures accurate filtering across the report.

---

## ✅ 4. Avoid Global Totals (or Make Them Manager-Only)

**Issue:**  
Totals like “All Sales” or “All Stock” can mislead users who only see partial data.

**Solutions:**
- Use RLS-safe measures:
```DAX
Total Sales (Secure) = 
CALCULATE([Total Sales], KEEPFILTERS(UserAccess[ItemCode]))
```
- OR create a **Manager-only page** with global metrics.

**Why:**  
Avoids misleading numbers and upholds RLS intent.

---

## ✅ 5. Create Role-Based Report Pages (Optional)

**Action:**
- Duplicate main pages.
- Tailor views per role:
  - SalesRep → Sales by Item
  - StockClerk → Inventory trends
  - Procurement → Purchases + Lead Times

**Why:**  
Improves navigation and reduces clutter for each user type.

---

## ✅ 6. Add a README or Info Tab

**Content to include:**
- Role definitions
- What each user can see
- Who to contact for access

**Why:**  
Enhances documentation and helps new users understand access limitations.

---

## ✅ Summary of Enhancements

| Task                        | What to Do                                     | Why It Matters                          |
|-----------------------------|-----------------------------------------------|------------------------------------------|
| Add Current User Card       | Show `USERNAME()`                             | Confirm login identity and RLS status    |
| Show User Role (optional)   | Display role with DAX                         | Improve clarity and testing              |
| Audit filters on visuals    | Ensure RLS filtering flows via ItemCode       | Prevent data leakage                     |
| Handle totals carefully     | Restrict or secure KPI cards                  | Avoid misinterpretation                  |
| Tailor role-based pages     | Create dedicated role views                   | Improve user experience                  |
| Add documentation tab       | Add roles and support info                    | Transparency and usability               |
