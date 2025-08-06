---
title : "Hive Scripts – Tạo bảng"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 6.2</b> "
---
#### Hive Scripts – Tạo bảng
Script tạo bảng:
+ Tạo external table cho dữ liệu thô
+ Tạo external table cho dữ liệu đã chuyển đổi

#### 1. lấy NanoID
````
#để tìm nanoid (trong trường hợp này của tôi là 6aqqepemzy)
cat .env 
````
![S3](/images/5.Hive%20Scripts%20–%20Create%20tables/Hive%20Scripts%20–%20Create%20tables2.png)

#### 2. Script tạo bảng
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
  's3://emr-pipeline-6aqqepemzy/emr_pipeline/data/sales_data_raw/'      #thay đổi NanoID của bạn ở đây
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
  's3://emr-pipeline-6aqqepemzy/emr_pipeline/data/sales_data/'      #thay đổi NanoID của bạn ở đây
TBLPROPERTIES (
    'parquet.compression'='SNAPPY'
);

````
{{% notice warning %}}
Bạn sẽ phải thay đổi `emr-pipeline-[NanoID của bạn]` tại `LOCATION`
{{% /notice %}}

Mã SQL này tạo hai external table trong môi trường Hive để quản lý dữ liệu bán hàng được lưu trữ trong Amazon S3.

1. Xóa bảng sales_data_raw: Mã bắt đầu bằng việc xóa bảng sales_data_raw nếu nó tồn tại, đảm bảo không có xung đột với định nghĩa bảng mới.

2. Tạo bảng sales_data_raw:
- Bảng này lưu trữ dữ liệu bán hàng thô ở định dạng CSV. Nó bao gồm các trường khác nhau như region, country, item_type và các chỉ số bán hàng.
- Dữ liệu được xử lý như văn bản (STRING) cho hầu hết các trường.
- Thư viện OpenCSVSerde được sử dụng để đọc định dạng CSV, và dòng đầu tiên (header) được bỏ qua khi tải dữ liệu.

3. Tạo bảng sales_data:
- Bảng này được thiết kế cho dữ liệu bán hàng có cấu trúc ở định dạng Parquet, hiệu quả hơn cho phân tích.
- Nó sử dụng các kiểu dữ liệu cụ thể như date, INTEGER và DECIMAL để đảm bảo tính toàn vẹn dữ liệu tốt hơn.
- Thư viện ParquetHiveSerDe được sử dụng để đọc file Parquet, và dữ liệu được lưu trữ với nén SNAPPY để tối ưu hóa lưu trữ và hiệu suất.

Tóm lại, mã thiết lập hai bảng riêng biệt: một cho dữ liệu thô và một cho dữ liệu đã xử lý, tạo điều kiện thuận lợi cho quản lý và phân tích dữ liệu hiệu quả.