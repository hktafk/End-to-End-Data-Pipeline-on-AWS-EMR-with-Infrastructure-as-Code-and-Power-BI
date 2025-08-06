---
title : "Create emr_pipeline folder"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---
In this module we will create a folder named: "emr_pipeline" that will store scripts and raw data

{{% notice tip %}}
Make sure you are in the root directory of your project:
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

#### Paste the values of this file
[Link to the data](https://github.com/hktafk/End-to-End-Data-Pipeline-on-AWS-EMR-with-Infrastructure-as-Code-AWS-CDK-and-Power-BI/blob/main/emr_pipeline/data/sales_data_raw/sales_data.csv)

![S3](/images/3.AWS%20S3%20Bucket%20Deployment%20stack/AWS%20S3-3.png)


