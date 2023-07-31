### Module 6: Use DAX time intelligence functions in Power BI Desktop models

-   In DAX, time intelligence means modifying the filter context for date filters
-   They can help you answer these time-related questions:
    -   What's the accumulation of revenue for the year, quarter, or month?
    -   What revenue was produced for the same period last year?
    -   What growth in revenue has been achieved over the same period last year?
    -   How many new customers made their first order in each month?
    -   What's the inventory stock on-hand value for the company's products?
-   Requires `Date` table that meets the following requirement:
    -   The date table must be indicated as a date table
    -   Other obvious <a href="https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/2-functions">requirements</a>

## <b>Summarizations over time</b>

-   `DATESYTD` - Returns a single-column table that contains dates for the year-to-date (YTD) in the current filter context. This group also includes the DATESMTD and DATESQTD DAX functions for month-to-date (MTD) and quarter-to-date (QTD). You can pass these functions as filters into the CALCULATE DAX function.
-   `DATESBETWEEN` - Returns a table that contains a column of dates that begins with a given start date and continues until a given end date.
-   `DATESINPERIOD` - Returns a table that contains a column of dates that begins with a given start date and continues for the specified number of intervals.
-   `TOTALYTD` - Evaluates an expression for YTD in the current filter context. The equivalent QTD and MTD DAX functions of `TOTALQTD` and `TOTALMTD` are also included.

## <b>Comparisons over time</b>

-   `DATEADD` - Returns a table that contains a column of dates, shifted either forward or backward in time by the specified number of intervals from the dates in the current filter context.
-   `PARALLELPERIOD` - Returns a table that contains a column of dates that represents a period that is parallel to the dates in the specified dates column, in the current filter context, with the dates shifted a number of intervals either forward in time or back in time.
-   `SAMEPERIODLASTYEAR` - Returns a table that contains a column of dates that are shifted one year back in time from the dates in the specified dates column, in the current filter context.
-   Many helper DAX functions for navigating backward or forward for specific time periods, all of which returns a table of dates. These helper functions include `NEXTDAY`, `NEXTMONTH`, `NEXTQUARTER`, `NEXTYEAR`, and `PREVIOUSDAY`, `PREVIOUSMONTH`, `PREVIOUSQUARTER`, and `PREVIOUSYEAR`.

## Calculate New Occurences

Another use of time intelligence functions is to count new occurrences. The following example shows how you can calculate the number of new customers for a time period. A new customer is counted in the time period in which they made their first purchase.

## Snapshot Calculations

Occasionally, fact data is stored as snapshots in time. Common examples include inventory stock levels or account balances. A snapshot of values is loaded into the table on a periodic basis.

```
Stock on Hand =
CALCULATE(
    SUM(Inventory[UnitsBalance]),
    LASTDATE('Date'[Date])
)
```

```
Stock on Hand =
CALCULATE(
    SUM(Inventory[UnitsBalance]),
    LASTNONBLANK(
        'Date'[Date],
        CALCULATE(SUM(Inventory[UnitsBalance]))
    )
)
```
