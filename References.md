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

