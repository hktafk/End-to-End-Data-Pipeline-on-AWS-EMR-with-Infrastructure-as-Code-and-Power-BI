---
title : "Tải PUTTY để SSH kết nối tới EMR Cluster"
date :  "`r Sys.Date()`" 
weight : 11
chapter : false
pre : " <b> 11. </b> "
---
Theo liên kết này:
[PUTTY](https://www.putty.org/)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.1.Downloading_PUTTY/Downloading%20PUTTY1.png?width=40pc)

Vậy Putty sẽ giúp chúng ta SSH trực tiếp vào EMR Cluster. 

Chúng ta cũng chuyển đổi file pem thành file ppk.

Mở thanh tìm kiếm và gõ: PUTTY gen.
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY1.png?width=40pc)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY2.png?width=40pc)
Conversions -> Import key

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY3.png?width=40pc)

Chọn file .pem

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY4.png?width=40pc)

Lưu private key
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.2.Configuring_PUTTY/Configuring%20PUTTY5.png?width=40pc)

Mở thanh tìm kiếm và gõ: PUTTY
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster1.png?width=40pc)

Trong AWS console, tìm public DNS
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster2.png?width=40pc)

Dán vào PUTTY
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster3.png)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster4.png)

Sau đó trong Session, Lưu lại. Để bạn không mất tất cả thông tin

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster5.png)

Sau đó chọn EMR và nhấp Open
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster6.png)

Sau đó nhấp Accept
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster7.png?width=40pc)

![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster8.png?width=40pc)

Đăng nhập với: Hadoop
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster9.png?width=40pc)

Bây giờ bạn có thể kết nối hive
````
hive
````
![PUTTY](/images/11.PUTTY_for_SSH_to_connect_to_EMR_Cluster/11.3.Connect_PUTTY_to_EMR_Cluster/Connect%20PUTTY%20to%20EMR%20Cluster10.png?width=40pc)