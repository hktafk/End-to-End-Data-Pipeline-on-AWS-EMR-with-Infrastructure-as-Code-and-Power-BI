---
title : "Hive Scripts – Transform Data"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 6.3</b> "
---
#### Hive Scripts – Transform Data
Create a transformation script:
+ ETL script fixes the dates in the sales data
+ Inserts the transformed data into the new table
#### 1. Create Transform script
````
code .\emr_pipeline\scripts\transform_data.hql
````

````
INSERT OVERWRITE TABLE sales_data
SELECT
    `region`,
    `country`,
    `item_type`,
    `sales_channel`,
    `order_priority`,
    CASE
      WHEN `order_date` RLIKE '([0-9]{2}\-[0-9]{2}\-[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`order_date` , 'MM-dd-yyyy')) AS DATE)
      WHEN `order_date` RLIKE '([0-9]{1,2}\/[0-9]{1,2}\/[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`order_date` , 'MM/dd/yyyy')) AS DATE)
      ELSE NULL
    END AS `order_date`,
    `order_id`,
    CASE
      WHEN `ship_date` RLIKE '([0-9]{2}\-[0-9]{2}\-[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`ship_date` , 'MM-dd-yyyy')) AS DATE)
      WHEN `ship_date` RLIKE '([0-9]{1,2}\/[0-9]{1,2}\/[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`ship_date` , 'MM/dd/yyyy')) AS DATE)
    END AS `ship_date`,
    CAST(`units_sold` AS INTEGER) AS units_sold,
    CAST(`unit_price` AS DECIMAL) AS unit_price,
    CAST(`unit_cost` AS DECIMAL) AS unit_cost,
    CAST(`total_revenue` AS DECIMAL) AS total_revenue,
    CAST(`total_cost` AS DECIMAL) AS total_cost,
    CAST(`total_profit` AS DECIMAL) AS total_profit 
FROM sales_data_raw
````
This SQL code is designed to load and transform data from the sales_data_raw table into the sales_data table.

1.	Insert Overwrite: The command replaces any existing data in the sales_data table with new data.

2.	Data Selection and Transformation:
- Various fields like region, country, and order_id are selected directly.
- The order_date and ship_date fields are checked for specific formats (MM-dd-yyyy or MM/dd/yyyy) using regular expressions and are converted to the proper DATE type.
- If the date format doesn't match, the values are set to NULL.
- Other numeric fields like units_sold, unit_price, and total_revenue are cast to appropriate types (INTEGER for whole numbers and DECIMAL for currency) for better data integrity.

3.	Source Table: The data is sourced from the sales_data_raw table, which contains unprocessed data.

In summary, this code cleans and formats the raw sales data, ensuring it is properly structured for analysis in the sales_data table.



