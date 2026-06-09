# Receivables Analytics - Key DAX Measures

These measures were developed to support receivables monitoring, aging analysis, collection tracking, and cash flow reporting.

---

## Due Outstanding Till End of Month

```DAX
Due Outstanding Till EOM =
CALCULATE(
    SUM(Receivables[Outstanding_Amount]),
    FILTER(
        Receivables,
        Receivables[Due_Date] < EOMONTH(TODAY(), 0)
    )
)
```

Calculates the total outstanding amount due before the end of the current month.

---

## Due Outstanding Till Today

```DAX
Due Outstanding Till Today =
CALCULATE(
    SUM(Receivables[Outstanding_Amount]),
    FILTER(
        Receivables,
        TODAY() > Receivables[Due_Date]
    )
)
```

Calculates all overdue outstanding amounts up to today's date.

---

## Outstanding Amount (0–30 Days)

```DAX
Outstanding 0-30 =
CALCULATE(
    SUM(Receivables[Outstanding_Amount]),
    FILTER(
        Receivables,
        Receivables[Age_Days] >= 0
            && Receivables[Age_Days] <= 30
    )
)
```

Calculates outstanding balances aged between 0 and 30 days.

---

## Current Month Collection

```DAX
Current Month Collection =
CALCULATE(
    [Total Collection],
    FILTER(
        Calendar,
        Calendar[Date] > [Previous Month End]
    )
)
```

Calculates collections received during the current month.

---

## Previous Month End

```DAX
Previous Month End =
EOMONTH(TODAY(), -1)
```

Returns the last date of the previous month.

---

## Invoice Value - 3 Months Back

```DAX
Invoice 3 Months Back =
CALCULATE(
    [Total Billing],
    FILTER(
        ALL(Calendar),
        EOMONTH(Calendar[Date], 0)
            = EOMONTH(TODAY(), -3)
    )
)
```

Calculates billing value from three months prior.

---

## Average Billing - Last 3 Months

```DAX
Average Billing Last 3 Months =
(
    [Invoice 3 Months Back]
    + [Invoice 2 Months Back]
    + [Invoice Last Month]
) / 3
```

Calculates average billing over the previous three months.

---

## Business Use Cases

These measures support:

- Receivables Aging Analysis
- Outstanding Amount Monitoring
- Collection Performance Tracking
- Cash Flow Visibility
- Billing Trend Analysis
- Overdue Receivable Identification
- Executive Finance Reporting
- Collection Planning & Forecasting
