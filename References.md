https://powerbi.microsoft.com/en-us/learning/

Prepare data for analysis
https://learn.microsoft.com/en-us/training/paths/prepare-data-power-bi/

# Learning Path: Get and transform data with Power BI

## Module 1: Get data in Power BI

##Top Ideas

-   Data sources can be from:

    -   Flat files (e.g. csv, xlsx, txt)
    -   Relational database (e.g. Connection via SQL server)
        -   SQL statements can be written to query specific datasets
        -   Best practice: Avoid writing SQL query directly in Power BI. Make a view instead.
        -   Dynamic reports can be built using parameters and embedding it in SQL query
    -   NoSQL database
    -   Online services
    -   Azure Analysis Services (PaaS that provides data model in the cloud)

-   Storage mode can either be import (save at workstation), direct query (make direct connection to the data source) or dual

-   Performance issues can be fixed/ managed by:

    -   Use Performance Analyzer tool
    -   Optimize performance using:
        -   Query folding
        -   Query diagnostic

-   Other techniques to optimize performance

    -   Process as much data as possible in the original data source.
    -   Use native SQL queries. When using DirectQuery for SQL databases, such as the case for our scenario, make sure that you aren't pulling data from stored procedures or common table expressions (CTEs).
    -   Separate date and time, if bound together. If any of your tables have columns that combine date and time, make sure that you separate them into distinct columns before importing them into Power BI. This approach will increase compression abilities.

-   Resolve data import errors

    -   Query timeout expired:

        -   Query at less busy time
        -   Pull less data

    -   Data type errors
        -   Cast/ convert the data

## Module 2: Clean, transform and load data in Power BI

Top Ideas

-   Power Query Editor enables you to transform imported data
-   All steps you made via PQE automatically applies whenever the data source connects to PowerBI
    -   Data can be unpivoted
    -   Pivot columns
-   Simplify the data structure
    -   Replace values (e.g. null)
    -   Remove duplicates
-   Evaluate and change column data types
    -   \*Power BI scans the first 1000 rows (for profiling purposes/ data detection/ among others)
    -   Incorrect data types affects the following:
        -   Prevent relationship
        -   Impede proper calculation
        -   Disrupt hierarchies
-   Combine multiple queries into a single table
    -   Append query
    -   Merge query
-   Profile data
    -   By default, only 1000 rows are profiled. This can be changed into <b>Column profiling based on ENTIRE data set</b>

# Learning Path: Model data with Power BI

## Module 1: Describe Power BI Desktop models

Top Ideas

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
