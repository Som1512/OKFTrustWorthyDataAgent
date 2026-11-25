---
type: Metric
title: Accounts Receivable Outstanding Balance
description: Unsettled customer balance across accounts receivable ledger transactions.
resource: WideworldimportersData/Sales.CustomerTransactions.csv
tags: [metric, finance, accounts-receivable, customers]
timestamp: 2026-11-23T15:38:00Z
---

# Definition

**Accounts Receivable Outstanding Balance** sums `OutstandingBalance` across open customer transactions in [Sales.CustomerTransactions](/tables/sales_customer_transactions.md), segmented by customer or [Sales.BuyingGroups](/tables/sales_buying_groups.md).

# Calculation

```sql
SELECT
  c.CustomerID,
  c.CustomerName,
  SUM(ct.OutstandingBalance) AS ar_outstanding_balance
FROM Sales.CustomerTransactions AS ct
JOIN Sales.Customers AS c
  ON ct.CustomerID = c.CustomerID
WHERE ct.IsFinalized = FALSE
GROUP BY c.CustomerID, c.CustomerName;
```

# Source Tables & Columns

- [Sales.CustomerTransactions](/tables/sales_customer_transactions.md): `OutstandingBalance`, `TransactionAmount`, `IsFinalized`, `CustomerID`
- [Sales.Customers](/tables/sales_customers.md): `CustomerID`, `CustomerName`, `BillToCustomerID`, `CreditLimit`
