---
title : "Whitelist IP to access HIVE"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 10.2 </b> "
---
In EC2, find and click on primary node 

![Whitelist IP to access HIVE](/images/10.How_to_access_EMR_Cluster/10.2.Whitelist_IP_to_access_HIVE/Whitelist%20IP%20to%20access%20HIVE1.png)

Edit inbound rules
Scroll down and click on “Add rule” -> All traffic -> My IP -> Save Rules
![Whitelist IP to access HIVE](/images/10.How_to_access_EMR_Cluster/10.2.Whitelist_IP_to_access_HIVE/Whitelist%20IP%20to%20access%20HIVE2.png)

![Whitelist IP to access HIVE](/images/10.How_to_access_EMR_Cluster/10.2.Whitelist_IP_to_access_HIVE/Whitelist%20IP%20to%20access%20HIVE3.png)


{{% notice note %}}
You have to have the pem key that access EMR Cluster in previous steps. We will need it later 
{{% /notice %}}
