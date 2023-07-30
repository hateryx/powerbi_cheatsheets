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
-   `TOTALYTD` - Evaluates an expression for YTD in the current filter context. The equivalent QTD and MTD DAX functions of TOTALQTD and TOTALMTD are also included.
-   `DATESBETWEEN` - Returns a table that contains a column of dates that begins with a given start date and continues until a given end date.
-   `DATESINPERIOD` - Returns a table that contains a column of dates that begins with a given start date and continues for the specified number of intervals.
