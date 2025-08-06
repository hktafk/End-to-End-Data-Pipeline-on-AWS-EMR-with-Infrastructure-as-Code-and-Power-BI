---
title : "Hive Scripts – Create tables"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 6.2</b> "
---
#### Hive Scripts – Create tables
Create tables script:
+ Create an external table for the raw data
+ Create an external table for the transformed data
#### 1. get the NanoID
````
#to find the nanoid (in this case mine is 6aqqepemzy)
cat .env 
````
![S3](/images/5.Hive%20Scripts%20–%20Create%20tables/Hive%20Scripts%20–%20Create%20tables2.png)

#### 2. Create table script
````
code .\emr_pipeline\scripts\create_tables.hql
````
![S3](/images/5.Hive%20Scripts%20–%20Create%20tables/Hive%20Scripts%20–%20Create%20tables1.png)

````
DROP TABLE sales_data_raw;
CREATE EXTERNAL TABLE sales_data_raw (
    `region` STRING,
    `country` STRING,
    `item_type` STRING,
    `sales_channel` STRING,
    `order_priority` STRING,
    `order_date` STRING,
    `order_id` STRING,
    `ship_date` STRING,
    `units_sold` STRING,
    `unit_price` STRING,
    `unit_cost` STRING,
    `total_revenue` STRING,
    `total_cost` STRING,
    `total_profit` STRING
)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.serde2.OpenCSVSerde'
LOCATION
  's3://emr-pipeline-6aqqepemzy/emr_pipeline/data/sales_data_raw/'      #change your NanoID here
TBLPROPERTIES (
    "skip.header.line.count"="1"
);

CREATE EXTERNAL TABLE sales_data (
    `region` STRING,
    `country` STRING,
    `item_type` STRING,
    `sales_channel` STRING,
    `order_priority` STRING,
    `order_date` date,
    `order_id` STRING,
    `ship_date` date,
    `units_sold` INTEGER,
    `unit_price` DECIMAL(10,2),
    `unit_cost` DECIMAL(10,2),
    `total_revenue` DECIMAL(12,2),
    `total_cost` DECIMAL(12,2),
    `total_profit` DECIMAL(12,2)
)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe'
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
  's3://emr-pipeline-6aqqepemzy/emr_pipeline/data/sales_data/'      #change your NanoID here
TBLPROPERTIES (
    'parquet.compression'='SNAPPY'
);

````
{{% notice warning %}}
You'll have to change `emr-pipeline-[your NanoID]` at `LOCATION`
{{% /notice %}}


This SQL code creates two external tables in a Hive environment for managing sales data stored in Amazon S3.
1.	Dropping the sales_data_raw Table: The code starts by dropping the sales_data_raw table if it exists, ensuring no conflicts with the new table definition.

2.	Creating sales_data_raw Table:
-	This table stores raw sales data in CSV format. It includes various fields like region, country, item_type, and sales metrics.
-	The data is treated as text (STRING) for most fields.
-	The OpenCSVSerde library is used to read the CSV format, and the first line (header) is skipped when loading data.

3.	Creating sales_data Table:
-	This table is designed for structured sales data in Parquet format, which is more efficient for analytics.
-	It uses specific data types like date, INTEGER, and DECIMAL for better data integrity.
-	The ParquetHiveSerDe library is used for reading Parquet files, and data is stored with SNAPPY compression to optimize storage and performance.


In summary, the code sets up two distinct tables: one for raw data and another for processed data, facilitating efficient data management and analysis.



