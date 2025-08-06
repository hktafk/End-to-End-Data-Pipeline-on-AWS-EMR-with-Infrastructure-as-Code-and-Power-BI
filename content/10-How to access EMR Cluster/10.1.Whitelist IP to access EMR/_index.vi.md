---
title : "Whitelist IP để truy cập EMR"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 10.1 </b> "
---
Tiếp theo bạn sẽ cần whitelist IP của mình để có thể truy cập EMR.

Đầu tiên hãy mở EC2 security group và nhấp vào Primary node
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR1.png)

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR2.png)

Cuộn xuống và thêm rule

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR3.png)

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR4.png)

SSH -> My IP -> Save rule

Bây giờ thử:
````
aws emr ssh --key-pair-file ~/ProjectProAlexClark.pem --cluster-id j-3SV9H2OBTRTDT
````

{{% notice warning %}}
Bạn sẽ phải thay đổi `ProjectProAlexClark.pem` và `j-3SV9H2OBTRTDT`
{{% /notice %}}

{{% notice note %}}
Bạn sẽ phải tìm thư mục home của mình và đặt ProjectProAlexClark (file keypair của bạn) ở đó.
{{% /notice %}}

{{% notice note %}}
Hoặc tìm nơi ProjectProAlexClark (file keypair của bạn) ở đâu và chạy lệnh như thế này:
````
aws emr ssh --key-pair-file "C:\Users\your\key\pair\directory\ProjectProAlexClark.pem" --cluster-id [your EMR cluster id]
````
{{% /notice %}}

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR5.png)

Cập nhật package:
````
sudo yum update
````

Sau đó mở hive
````
hive
````
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR6.png)

Với EMR mở, chúng ta có thể bắt đầu xem các bảng:
````
show tables;
````
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR7.png?width=40pc)

Xem giá trị bảng:
````
select * from sales_data_raw limit 10;
````
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR8.png)