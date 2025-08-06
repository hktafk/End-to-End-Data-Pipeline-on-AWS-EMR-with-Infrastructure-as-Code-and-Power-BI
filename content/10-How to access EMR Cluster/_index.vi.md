---
title : "Cách truy cập EMR Cluster"
date :  "`r Sys.Date()`" 
weight : 10
chapter : false
pre : " <b> 10. </b> "
---
Mở powershell mới:

![AccessEMRCluser](/images/10.How_to_access_EMR_Cluster/How%20to%20access%20EMR%20Cluster1.png?width=30pc)

Gõ:
````
aws emr ssh --key-pair-file ~/ProjectProAlexClark.pem --cluster-id j-3SV9H2OBTRTDT
````
{{% notice warning %}}
Bạn sẽ phải thay đổi `ProjectProAlexClark.pem` và `j-3SV9H2OBTRTDT`
{{% /notice %}}

{{% notice tip %}}
bạn có thể lấy Cluster id và Key pair trong EC2 
{{% /notice %}}

![AccessEMRCluser](/images/10.How_to_access_EMR_Cluster/How%20to%20access%20EMR%20Cluster2.png?width=90pc)

![AccessEMRCluser](/images/10.How_to_access_EMR_Cluster/How%20to%20access%20EMR%20Cluster3.png?width=90pc)