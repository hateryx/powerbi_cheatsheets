# Learning Path: Model data with Power BI

## Module 1: Describe Power BI Desktop models

### Top Ideas

-   Optimal models are important for delivering good query performance and for minimizing data refresh times
-   Star Schema Design
    -   Fact tables
        -   Purpose is to summarize
    -   Dimension tables
        -   Purpose is to query and group
-   Analytic queries
    -   Produces query result from data model
    -   Typically undergoes three phases
        -   Filter
            -   Entire report
            -   Specific page
            -   Specific visual
        -   Group
        -   Summarize
-   Measures

    -   Designed to summarize model data

-   Star Schema
    -   Mature modeling approach widely adopted by relational data warehouses
    -   Classify tables whether it is dimension or fact

## Module 2: Choose a Power BI model framework

### Top Ideas

-   Power BI model fundamentals

    -   Power BI Data Model
        -   Querable using DAX or MDX
        -   Power BI data model published in workspace => Power BI dataset
        -   Is a tabular model (model comprises of table)
    -   Import model
        -   Benefits
            -   Stored entirely in memory = Best query performance
        -   Limitations
            -   1 GB Limit per dataset
        -   Optimization best practices
            -   Reduce data stored in the table by:
                -   Group by and summarize to raise the grain of fact tables
                -   Prefer numeric data type
                -   Prefer custom column in Power Query instead of calculated column
                -   Disable Power Query load
                -   Disable auto date/time
    -   Direct Query model
        -   Benefits
            -   Optimized for large data sources
            -   Create specialized datasets
        -   Limitations
            -   Power Query (M) transformations are not possible
            -   Analytic queries can impact on source system performance (i.e. server/ database)
    -   Composite Model
        -   For recheck at https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/5-determine-when-to-develop-composite-model

-   Choosing a model framework

    -   Choose the import model whenever possible
    -   Direct Query model fits best if your report needs real time data OR data source stores large volume of data
    -   Composite model is preferred for:
        -   Boosting the query performance of a Direct Query model
        -   Deliver near real time result from an import model
        -   Extend a Power BI dataset (or AAS model) with additional data
    -   Hybrid tables
    -   Aggregation table
    -   Plan carefully. In Power BI Desktop, it’s always possible to convert a DirectQuery table to an import table. But it’s not possible to convert an import table to a DirectQuery table.

-   A composite model would comprise a DirectQuery source group containing the sales dataset tables, and an import source group containing the imported web page data.
-   A hybrid table includes a DirectQuery partition for the current period to deliver near-real time results.
-   Setting the related dimension tables to dual storage mode will allow Power BI to satisfy higher-grain queries entirely from cache.

## Module 3: Design a data model in Power BI

### Top Ideas

-   Building a great data model is about simplifying the disarray.
-   Choose the correct granularity
-   Dimension tables are used to filter and group the data in fact tables.
-   Flatten parent-child hierarchy
    -   The process of viewing multiple child levels based on a top-level parent is known as flattening the hierarchy. In this process, you are creating multiple columns in a table to show the hierarchical path of the parent to the child in the same record. You will use PATH(), a simple DAX function that returns a text version of the managerial path for each employee, and PATHITEM() to separate this path into each level of managerial hierarchy.
-   Data Granularity - means the level of detail in the data
-   Cross filter direction
    -   You might have lower performance when using bi-directional cross-filtering with many-to-many relationships.

## Module 4: Write DAX formulas for Power BI Desktop models

### Top Ideas

-   DAX Formulas covers the following types of calculations:
    -   Calculated tables
        -   Duplicate/ transform <i>existing</i> series of data into a new table
        -   Increases model storage size
        -   Can be useful for:
            -   Role playing dimensions
                -   Useful when two tables have multiple relationships
                -   For example, `Sales` table with `ShipDate` and `OrderDate` column will have multiple relationships to the `Dates` table, specifically the `Date` column. For better model design, the `Dates` table can be duplicated into another table (called as `Ship Dates`) to have dedicated relationship with `ShipDate` column.
            -   Date tables
                -   If you do not have a date table, you can create one using calc table
            -   What-if analysis
                -   `Learning debt`
    -   Calculated columns
    -   Measures
        -   Summarization over model data
        -   Results are not stored in the model
        -   Not available in the Power Query
-   About DAX Formulas
    -   Calculated measures
        -   Returns scalar value (single value)
    -   Calculated table
        -   Returns table object
    -   Formulas are assembled by using:
        -   DAX Functions
        -   DAX Operators
        -   References to model objects
        -   Column References
            -   `Table[Column]`
        -   Measure References
            -   `[Measure]`
        -   DAX Variables
        -   Whitespace
-   Data Types
    -   Column data types are defined from Power Query
    -   Measure and Calculated Columns are implicitly defined from formula
    -   Blank = NULL
-   DAX Variables !
    -   Use `VAR` to declare a variable then use `RETURN` for the output
    -   ```
        Revenue YoY % =
            VAR RevenuePriorYear =
                CALCULATE(
                    [Revenue],
                    SAMEPERIODLASTYEAR('Date'[Date])
                )
            RETURN
                DIVIDE(
                    [Revenue] - RevenuePriorYear,
                    RevenuePriorYear
                )
        ```

## Module 5: Add Measures to the Power BI Desktop Models

### Top Ideas

-   Implicit measures
    -   These come from aggregation functions on columns
    -   The most significant limitation of implicit measures is that they only work for simple scenarios, meaning that they can only summarize column values that use a specific aggregation function
-   Explicit Measures
    -   Created via DAX Formula
    -   Simple Measures
        -   Aggregates single column or single table
    -   Compounded Measures
        -   Nesting measures
        -   This can be used to do away with calculated columns and use measure to optimize data
-   Difference between calculated columns and measures

|            | Calculated Columns                          | Measures                          |
| ---------- | ------------------------------------------- | --------------------------------- |
| Evaluation | Uses row context at data refresh time       | Uses filter context at query time |
| Purpose    | Extends a column                            | Summarize model data              |
| Storage    | Store a value for each row                  | Never store a value               |
| Visual Use | Can be used for Filter, Summarize and Group | Designed to summarize             |

## Module 5: Add Calculated tables and columns to Power BI Desktop models

### Top Ideas

-   Calculated table
    -   Use case
        -   Duplicate table for role playing dimensions
        -   Create date table
    -   Disadvantages
        -   Increase model storage size
        -   Prolong data refresh time
-   Row context
    -   Does not extend beyond the table
        ```
        Due Fiscal Year =
        "FY" & YEAR('Due Date'[Due Date])
        + IF(
            MONTH('Due Date'[Due Date]) <= 6,
            1
        )
        ```
    -   If your formula needs to reference columns in other tables, you have two options:
        -   If the tables are related, directly or indirectly, you can use the ` RELATED` or `RELATEDTABLE` DAX function.
            -   The `RELATED` function retrieves the value at the one-side of the relationship. (Recommended)
                `Example:`
                ```
                Discount Amount =
                (Sales[Order Quantity]
                    * RELATED('Product'[List Price])
                ) - Sales[Sales Amount]
                ```
            -   The `RELATEDTABLE` retrieves values on the many-side.
        -   When the tables aren't related, you can use the `LOOKUPVALUE` DAX function.
    -   Row context is used when calculated column formulas are evaluated. It's also used when a class of functions, known as <i>iterator</i> functions, are used.
-   3 Techniques To Add A Column

    -   Add columns to a view or table (as a persisted column), and then source them in Power Query. This option only makes sense when your data source is a relational database and if you have the skills and permissions to do so. However, it's a good option because it supports ease of maintenance and allows reuse of the column logic in other models or reports.
    -   Add custom columns (using M) to Power Query queries. `Preferred`. Optimal load.
    -   Add calculated columns (using DAX) to model tables.

-   When to use a calculated column in place of a Power Query custom column.

    -   Depends on summarized model data.
    -   Needs to use specialized modeling functions that are only available in DAX, such as the `RELATED` and `RELATEDTABLE` functions. Specialized functions can also include the <a href="https://learn.microsoft.com/en-us/dax/understanding-functions-for-parent-child-hierarchies-in-dax">DAX parent and child hierarchies</a>, which are designed to naturalize a recursive relationship into columns, for example, in an employee table where each row stores a reference to the row of the manager (who is also an employee). <a href="https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/4-technique">Cheat Reference</a>
