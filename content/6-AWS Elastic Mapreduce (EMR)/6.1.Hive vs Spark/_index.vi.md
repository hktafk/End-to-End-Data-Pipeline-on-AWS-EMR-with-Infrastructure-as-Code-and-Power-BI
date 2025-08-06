---
title : "Hive vs Spark"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 6.1 </b> "
---
#### Hive vs Spark
2 công cụ được sử dụng nhiều nhất hiện nay để xử lý big data là hive và spark, nhưng spark gần đây ngày càng phổ biến hơn, vượt trội hive trong nhiều trường hợp (ví dụ: Tốc độ).

| Spark                                                                                                             | Hive                                                                        |
|-------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| Hệ thống kho dữ liệu để truy vấn và phân tích các bộ dữ liệu lớn được lưu trữ trong Hadoop Distributed File System (HDFS) | Spark, mặt khác, là một engine xử lý big data nhanh và linh hoạt |
| Được thiết kế cho xử lý batch và được tối ưu hóa cho các truy vấn chạy lâu trên các bộ dữ liệu lớn.                     | Khối lượng công việc xử lý batch và thời gian thực.                                   |
| Rất ổn định                                                                                                       | Đường cong học tập dốc hơn, đặc biệt là từ SQL                          |
| Dễ học hơn vì Hive Query Language (HQL) rất giống với SQL                                            | Hỗ trợ đa ngôn ngữ bao gồm Python, Scala, Java                        |