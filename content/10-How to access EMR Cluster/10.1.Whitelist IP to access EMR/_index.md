---
title : "Whitelist IP to access EMR"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 10.1 </b> "
---
Next you will need to whitelist your IP so that you can access EMR.


First let’s open up EC2 security group and click on Primary node
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR1.png)

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR2.png)

Scroll down and add rule

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR3.png)

![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR4.png)

SSH -> My IP -> Save rule

Now try:
````
aws emr ssh --key-pair-file ~/ProjectProAlexClark.pem --cluster-id j-3SV9H2OBTRTDT
````

{{% notice warning %}}
You'll have to change `ProjectProAlexClark.pem` and `j-3SV9H2OBTRTDT`
{{% /notice %}}

{{% notice note %}}
You’ll have to find your home directory and put ProjectProAlexClark (your keypair file) there. 
{{% /notice %}}



{{% notice note %}}
Or find where ProjectProAlexClark (your keypair file) is and run command like this:
````
aws emr ssh --key-pair-file "C:\Users\your\key\pair\directory\ProjectProAlexClark.pem" --cluster-id [your EMR cluster id]
````
{{% /notice %}}


![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR5.png)

Update package:
````
sudo yum update
````

Then open hive
````
hive
````
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR6.png)

With EMR open we can start to see tables:
````
show tables;
````
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR7.png?width=40pc)

See table values:
````
select * from sales_data_raw limit 10;
````
![Whitelist IP to access EMR](/images/10.How_to_access_EMR_Cluster/10.1.Whitelist_IP_to_access_EMR/10.1.Whitelist%20IP%20to%20access%20EMR8.png)





