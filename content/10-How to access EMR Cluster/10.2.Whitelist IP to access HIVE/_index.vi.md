---
title : "Whitelist IP để truy cập HIVE"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 10.2 </b> "
---
Trong EC2, tìm và nhấp vào primary node 

![Whitelist IP to access HIVE](/images/10.How_to_access_EMR_Cluster/10.2.Whitelist_IP_to_access_HIVE/Whitelist%20IP%20to%20access%20HIVE1.png)

Chỉnh sửa inbound rules
Cuộn xuống và nhấp vào "Add rule" -> All traffic -> My IP -> Save Rules
![Whitelist IP to access HIVE](/images/10.How_to_access_EMR_Cluster/10.2.Whitelist_IP_to_access_HIVE/Whitelist%20IP%20to%20access%20HIVE2.png)

![Whitelist IP to access HIVE](/images/10.How_to_access_EMR_Cluster/10.2.Whitelist_IP_to_access_HIVE/Whitelist%20IP%20to%20access%20HIVE3.png)

{{% notice note %}}
Bạn phải có pem key để truy cập EMR Cluster trong các bước trước. Chúng ta sẽ cần nó sau này
{{% /notice %}}