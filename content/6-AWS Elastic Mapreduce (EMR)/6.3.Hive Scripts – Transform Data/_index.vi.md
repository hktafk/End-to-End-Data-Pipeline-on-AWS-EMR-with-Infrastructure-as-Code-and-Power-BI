---
title : "Hive Scripts – Chuyển đổi Dữ liệu"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 6.3</b> "
---
#### Hive Scripts – Chuyển đổi Dữ liệu
Tạo script chuyển đổi:
+ Script ETL sửa các ngày tháng trong dữ liệu bán hàng
+ Chèn dữ liệu đã chuyển đổi vào bảng mới

#### 1. Tạo script Transform
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
      WHEN `order_date` RLIKE '([0-9]{2}\\-[0-9]{2}\\-[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`order_date` , 'MM-dd-yyyy')) AS DATE)
      WHEN `order_date` RLIKE '([0-9]{1,2}\\/[0-9]{1,2}\\/[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`order_date` , 'MM/dd/yyyy')) AS DATE)
      ELSE NULL
    END AS `order_date`,
    `order_id`,
    CASE
      WHEN `ship_date` RLIKE '([0-9]{2}\\-[0-9]{2}\\-[0-9]{4})'
        THEN CAST(from_unixtime(unix_timestamp(`ship_date` , 'MM-dd-yyyy')) AS DATE)
      WHEN `ship_date` RLIKE '([0-9]{1,2}\\/[0-9]{1,2}\\/[0-9]{4})'
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

Mã SQL này được thiết kế để tải và chuyển đổi dữ liệu từ bảng sales_data_raw vào bảng sales_data.

1. Insert Overwrite: Lệnh thay thế bất kỳ dữ liệu hiện có nào trong bảng sales_data bằng dữ liệu mới.

2. Lựa chọn và Chuyển đổi Dữ liệu:
- Các trường khác nhau như region, country và order_id được chọn trực tiếp.
- Các trường order_date và ship_date được kiểm tra các định dạng cụ thể (MM-dd-yyyy hoặc MM/dd/yyyy) bằng regular expressions và được chuyển đổi thành kiểu DATE phù hợp.
- Nếu định dạng ngày không khớp, các giá trị được đặt thành NULL.
- Các trường số khác như units_sold, unit_price và total_revenue được cast thành các kiểu phù hợp (INTEGER cho số nguyên và DECIMAL cho tiền tệ) để đảm bảo tính toàn vẹn dữ liệu tốt hơn.

3. Bảng Nguồn: Dữ liệu được lấy từ bảng sales_data_raw, chứa dữ liệu chưa được xử lý.

Tóm lại, mã này làm sạch và định dạng dữ liệu bán hàng thô, đảm bảo nó được cấu trúc đúng cách để phân tích trong bảng sales_data.