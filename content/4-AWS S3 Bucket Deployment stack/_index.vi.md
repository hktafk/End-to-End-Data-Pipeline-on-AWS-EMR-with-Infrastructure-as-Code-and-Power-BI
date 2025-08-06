---
title : "AWS S3 Bucket Deployment stack"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
#### Tạo bucket deployment stack:
- Stack này chứa tất cả tài nguyên AWS liên quan đến việc tạo bucket, lưu trữ dữ liệu trong S3.
- Chúng ta có **primary bucket** cho mọi thứ trong dự án này.
- Chúng ta có **log_bucket** (emr logs) đây là best practice vì bạn nên lưu trữ log riêng biệt khỏi storage chính.	
- Chúng ta có bucket deployment construct lấy tất cả các file trong **emr_pipeline** (mà chúng ta sẽ tạo sau) và upload chúng lên S3.


### Nội dung:
<!--
   - [Cập nhật IAM Role](./4.1-updateiamrole/)
   - [Tạo **S3 Bucket**](./4.2-creates3bucket/)
   - [Tạo S3 Gateway endpoint](./4.3-creategwes3)
   - [Cấu hình **Session logs**](./4.4-configsessionlogs/)
-->