---
title : "Cấu hình AWS CLI"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.1.2 </b> "
---
Đăng nhập bằng IAM user:
- [Tạo AWS access key](https://www.geeksforgeeks.org/cloud-computing/)
![AWS CLI](/images/1.Setup/Setup5.png?width=90pc)

Làm theo hướng dẫn này để tạo access key:

- [Tạo AWS access key](https://www.geeksforgeeks.org/cloud-computing/how-to-create-aws_access_key-and-seceret-key/)

{{% notice note %}}
bỏ qua điều này nếu bạn đã có access key
{{% /notice %}}

Tạo access key mới và tải xuống thành file csv:
![AWS CLI](/images/1.Setup/Setup6.png?width=90pc)

Nếu bạn đã có AWS Access Key ID: 
- Nhấp vào tìm kiếm
- gõ "cmd"
- Nhấp chuột phải -> Run as administrator
- gõ: "aws configure"

![AWS CLI](/images/1.Setup/Setup4.png?width=40pc)

Điền tất cả thông tin của tài khoản AWS của bạn:
![AWS CLI](/images/1.Setup/Setup7.png?width=40pc)