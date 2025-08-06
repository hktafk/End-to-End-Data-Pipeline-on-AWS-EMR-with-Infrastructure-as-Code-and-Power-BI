---
title : "Tạo thư mục emr_pipeline"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---
Trong module này chúng ta sẽ tạo một thư mục có tên: "emr_pipeline" để lưu trữ scripts và dữ liệu thô

{{% notice tip %}}
Đảm bảo bạn đang ở thư mục gốc của dự án:
{{% /notice %}}

````
mkdir emr_pipeline
````
![S3](/images/3.AWS%20S3%20Bucket%20Deployment%20stack/AWS%20S3-1.png)

````
cd .\emr_pipeline\
mkdir data
mkdir scripts
````
![S3](/images/3.AWS%20S3%20Bucket%20Deployment%20stack/AWS%20S3-2.png)

````
mkdir data/sales_data_raw/
code data/sales_data_raw/sales_data.csv
````

#### Dán các giá trị của file này
[Đây là liên kết github](https://github.com/Prashant501Tyagi/-Build-an-ETL-Pipeline-on-EMR-using-AWS-CDK-and-Power-BI/blob/Main/emr_pipeline/data/sales_data_raw/sales_data.csv?plain=1)

![S3](/images/3.AWS%20S3%20Bucket%20Deployment%20stack/AWS%20S3-3.png)