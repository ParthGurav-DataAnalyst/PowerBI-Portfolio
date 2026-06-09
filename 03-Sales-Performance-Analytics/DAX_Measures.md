# Sales Performance Analytics - Key DAX Measures

These measures were developed to support sales performance monitoring, target achievement analysis, and year-over-year sales comparisons.

---

## Financial Year

```DAX
Financial Year =
IF(
    MONTH(Sales[Invoice_Date]) >= 4,
    YEAR(Sales[Invoice_Date]),
    YEAR(Sales[Invoice_Date]) - 1
)
```

Creates a custom financial year based on the April–March fiscal calendar. Transactions from April onwards belong to the current financial year, while January–March are assigned to the previous financial year.

---

## Total Sales Amount

```DAX
M_Amount =
SUM(Sales[Sales_Amount])
```

Calculates total sales revenue.

---

## Current Year Sales

```DAX
Current Year Sales =
CALCULATE(
    [M_Amount],
    FILTER(
        Sales,
        YEAR(Sales[Invoice_Date]) = 2026
    ),
    REMOVEFILTERS(Sales[Invoice_Date].[Month])
)
```

Calculates total sales for the selected fiscal year.

---

## Last Year Sales Till Current Month

```DAX
Last Year Till Month =
VAR CurrentYear =
    YEAR(TODAY())

VAR CurrentMonth =
    MONTH(TODAY())

RETURN
CALCULATE(
    [M_Amount],
    FILTER(
        Sales,
        YEAR(Sales[Invoice_Date]) = CurrentYear - 1
            && MONTH(Sales[Invoice_Date]) <= CurrentMonth
    )
)
```

Calculates cumulative sales from last year up to the current month.

---

## Today's Sales

```DAX
Today's Sales =
CALCULATE(
    [M_Amount],
    FILTER(
        Sales,
        Sales[Invoice_Date] = TODAY()
    )
)
```

Calculates total sales generated today.

---

## Current Month Sales

```DAX
Current Month Sales =
CALCULATE(
    [M_Amount],
    FILTER(
        Sales,
        YEAR(Sales[Invoice_Date]) = YEAR(TODAY())
            && MONTH(Sales[Invoice_Date]) = MONTH(TODAY())
    )
)
```

Calculates total sales for the current month.

---

## Same Month Last Year

```DAX
Same Month Last Year =
VAR CurrentYear =
    YEAR(TODAY())

VAR CurrentMonth =
    MONTH(TODAY())

RETURN
CALCULATE(
    [M_Amount],
    FILTER(
        Sales,
        YEAR(Sales[Invoice_Date]) = CurrentYear - 1
            && MONTH(Sales[Invoice_Date]) = CurrentMonth
    ),
    REMOVEFILTERS(Sales[Invoice_Date].[Year])
)
```

Calculates sales for the same month in the previous year.

---

## Business Use Cases

These measures support:

- Financial Year Reporting
- Sales KPI Monitoring
- Monthly Revenue Analysis
- Year-over-Year Comparisons
- Current Month Performance Tracking
- Daily Sales Monitoring
- Executive Sales Reporting
- Target Achievement Analysis
