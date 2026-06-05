
# Warehouse Inventory Optimization — SQL Analysis

Analyzed $52,839 inventory across 4 warehouses to identify cash concentration risks, dead stock, and reorder optimization opportunities using Advanced SQL.

**Business Goal**: Convert raw inventory data into actionable recommendations to free working capital and reduce stockout risk.

**Tools**: MySQL, CTEs, Window Functions, DENSE_RANK()

---

## 📊 Key Business Questions Answered

| # | Business Question | SQL Technique | Key Finding | Action |
| --- | --- | --- | --- | --- |
| 1 | What items are below reorder level with inactive suppliers? | `WHERE` + Calculated Column | 3 items at risk. Total restock cost = $3,300 | Expedite PO or find new suppliers |
| 2 | Where is our cash concentrated? | `SUM() OVER()`, `CTE` | Control Panels (West) = $9,600 = 18.17% of total | Monitor West warehouse closely |
| 3 | How much capital is stuck in dead stock? | `FILTER` + Business Logic | 13 SKUs = $21,311 overstock. 18 have Active suppliers | Run promo to liquidate $21K |
| 4 | Which items lose margin after overhead? | `WHERE` + Math | 4 items >$100 after 15% overhead. Control Panels = $920 | Review pricing on high-cost items |
| 5 | What is the #1 cash item per warehouse? | `DENSE_RANK() PARTITION BY` | West: Control Panels $9.6K, East: Fasteners $4.2K | Adjust reorder levels per location |

---

## 💡 Executive Summary

**Total Inventory Value**: $52,839 across North, South, East, West  
**Biggest Risk**: West warehouse Control Panels = $9,600 in single SKU  
**Biggest Opportunity**: $21,311 dead stock with Active suppliers = can liquidate to cash  
**Quick Win**: Reduce safety stock 30% on top-ranked Active supplier items
  AND supplier_status != 'Active'
ORDER BY Restock_Cost DESC;
