# Power BI DAX Measures

### Total Sales YTD
```dax
Total Sales YTD = 
CALCULATE(
    SUM(Sales[SalesAmount]),
    DATESYTD(DimDate[Date])
)
```
