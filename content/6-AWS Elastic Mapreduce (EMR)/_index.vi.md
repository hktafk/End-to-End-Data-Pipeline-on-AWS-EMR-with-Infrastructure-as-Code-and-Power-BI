---
title : "AWS Elastic Mapreduce"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
#### AWS Elastic Mapreduce (EMR)

AWS EMR là một framework phân tán sẽ xử lý big data, giống như các công cụ big data khác như Apache Hive, Hadoop, Spark….

Bạn có thể đọc thêm về điều đó [TẠI ĐÂY](https://www.bing.com/search?pglt=929&q=AWS+Elastic+Mapreduce+(EMR)&gs_lcrp=EgRlZGdlKgYIABBFGDkyBggAEEUYOTIGCAEQRRhA0gEHODE1ajBqMagCALACAA&PC=WSEDSE). Nói ngắn gọn, đây là một công cụ có thể chứa nhiều **cluster**, một **cluster** có thể chứa nhiều node hoặc đơn vị tính toán, và mỗi node có thể xử lý một phần dữ liệu rồi tập hợp lại để tạo ra kết quả. Với loại framework này, chúng ta có thể xử lý **BIG DATA** (như hàng trăm Terabyte).

AWS EMR được sử dụng trong nhiều tác vụ big data:
+ thu thập dữ liệu
+ xử lý dữ liệu
+ chuyển đổi dữ liệu 
+ phân tích dữ liệu
+ machine learning 
+ Spark streaming (dữ liệu thời gian thực)


- AWS EMR cũng có khả năng mở rộng cao (dễ dàng thêm hoặc xóa node khỏi cluster)
- Các tính năng bảo mật đa dạng, chẳng hạn như mã hóa dữ liệu trong quá trình truyền tải và lưu trữ, và kiểm soát truy cập chi tiết.
- EMR có thể tích hợp với các dịch vụ AWS khác, và có thể dễ dàng sử dụng kết hợp với các dịch vụ big data AWS khác, chẳng hạn như Amazon Redshift và Amazon Athena.
- EMR cũng cung cấp các công cụ quản lý và giám sát khác nhau, chẳng hạn như Amazon CloudWatch, AWS CloudTrail và AWS Management Console, để giúp người dùng quản lý và giám sát quy trình làm việc big data của họ.