---
title : "How to access EMR Cluster"
date :  "`r Sys.Date()`" 
weight : 10
chapter : false
pre : " <b> 10. </b> "
---
Open a new powershell:

![AccessEMRCluser](/images/10.How_to_access_EMR_Cluster/How%20to%20access%20EMR%20Cluster1.png?width=30pc)

Type:
````
aws emr ssh --key-pair-file ~/ProjectProAlexClark.pem --cluster-id j-3SV9H2OBTRTDT
````
{{% notice warning %}}
You'll have to change `ProjectProAlexClark.pem` and `j-3SV9H2OBTRTDT`
{{% /notice %}}

{{% notice tip %}}
you could get your Cluster id and Key pair in EC2 
{{% /notice %}}

![AccessEMRCluser](/images/10.How_to_access_EMR_Cluster/How%20to%20access%20EMR%20Cluster2.png?width=90pc)

![AccessEMRCluser](/images/10.How_to_access_EMR_Cluster/How%20to%20access%20EMR%20Cluster3.png?width=90pc)
