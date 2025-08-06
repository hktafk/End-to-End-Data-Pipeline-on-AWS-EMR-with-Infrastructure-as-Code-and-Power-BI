---
title : "Download PUTTY for SSH to connect to EMR Cluster"
date :  "`r Sys.Date()`" 
weight : 11
chapter : false
pre : " <b> 11. </b> "
---
Follow this link:
[PUTTY](https://www.putty.org/)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.1.Downloading_PUTTY/Downloading%20PUTTY1.png?width=40pc)

So Putty will help us SSH straight into EMR Cluster. 

We also Convert pem file into ppk file.

Open Search bar and type: PUTTY gen.
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY1.png?width=40pc)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY2.png?width=40pc)
Conversions -> Import key

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY3.png?width=40pc)

Choose the .pem file

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY4.png?width=40pc)

Save private key
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY5.png?width=40pc)

Open Search bar and type: PUTTY
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster1.png?width=40pc)

In AWS console, find public DNS
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster2.png?width=40pc)

Paste that into PUTTY
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster3.png)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster4.png)

Then in Session, Save it. So that you can’t lose all the information

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster5.png)

Then Choose EMR and click Open
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster6.png)

Then click Accept
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster7.png?width=40pc)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster8.png?width=40pc)

Login as: Hadoop
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster9.png?width=40pc)

You now can connect hive
````
hive
````
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster10.png?width=40pc)

