POWER BI RETAIL SALES COMPREHENSIVE CAPSTONE
Scenario: fictional multi-region retailer | Date range: 2023-2025
Synthetic training data only; example.com emails are fictional.
Use this dataset separately from the earlier small retail mini-project. Do not merge the datasets.

FILES / ROW COUNTS
Customers.csv: 1,500
Products.xlsx: 120
Employees.xlsx: 45
Orders.csv: 12,000
Order_Items.csv: 28,641
SalesTargets.csv: 1,620
Returns.csv: 1,239

KEY MODEL RELATIONSHIPS (1:* unless noted)
Customers[CustomerID] -> Orders[CustomerID]
Employees[EmployeeID] -> Orders[SalespersonID]
Orders[OrderID] -> Order_Items[OrderID]
Products[ProductID] -> Order_Items[ProductID]
Employees[EmployeeID] -> SalesTargets[EmployeeID]
Calendar[Date] -> Orders[OrderDate] (active)
Calendar[Date] -> SalesTargets[MonthStart] (active; target dates are month starts)
Order_Items[OrderItemID] -> Returns[OrderItemID]
For return-date analysis, add a separate/role-playing date relationship to Returns[ReturnDate] or use USERELATIONSHIP.

IMPORTANT MEASURES
Net Sales = SUM(Order_Items[NetSales])
Gross Sales = SUM(Order_Items[GrossSales])
Discount = SUM(Order_Items[DiscountAmount])
Total Cost = SUM(Order_Items[TotalCost])
Gross Profit = [Net Sales] - [Total Cost]
Gross Margin % = DIVIDE([Gross Profit],[Net Sales])
Units Sold = SUM(Order_Items[Quantity])
Orders = DISTINCTCOUNT(Orders[OrderID])
Average Order Value = DIVIDE([Net Sales],[Orders])
Revenue Target = SUM(SalesTargets[RevenueTarget])
Target Attainment % = DIVIDE([Net Sales],[Revenue Target]) (validate filter context and target grain before final use)
Returned Units = SUM(Returns[ReturnedQuantity])

MODEL CAUTION
Orders and Order_Items have different grains (order header vs line). Do not sum header-level fields after expanding them to line-item grain. Returns is a sampled synthetic returns table linked by OrderItemID; treat return measures carefully and do not interpret as a precise real-world benchmark.

SUGGESTED REPORT PAGES
1 Executive Overview
2 Sales Performance & Targets
3 Product and Category Analysis
4 Customer Insights
5 Sales Team Performance
6 Returns & Operations
7 Order Detail / Drill-through

Data quality and key validation should be included as project tasks. Create a Calendar table in Power BI covering the required date range, then mark it as a date table.
