---
title : "Thiết lập Visual Studio Code + bộ công cụ"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.2.1 </b> "
---
#### 1.Cài đặt Visual Studio Code
Sử dụng liên kết bên dưới để tải xuống Visual Studio Code:
- [Tải Visual Studio Code](https://code.visualstudio.com/)
![Visual Studio Code](/images/1.Setup/Setup32.png?width=90pc)

#### 2.Cài đặt bộ công cụ Visual Studio Code
Sử dụng liên kết bên dưới để tải xuống bộ công cụ Visual Studio Code:
- [Tải bộ công cụ](https://aws.amazon.com/visualstudiocode/)
![Visual Studio Code](/images/1.Setup/Setup8.png?width=90pc)

{{% notice info %}}
liên kết sẽ mở cửa sổ extensions VS Code, cài đặt AWS Toolkit:
{{% /notice %}}
![Visual Studio Code](/images/1.Setup/Setup9.png?width=90pc)

Khi hoàn thành, đăng nhập bằng "IAM Credentials"
![Visual Studio Code](/images/1.Setup/Setup10.png?width=90pc)

{{% notice info %}}
Bạn có thể lấy Profile name trong AWS Console, Access key và Secret Key ở bước trước
{{% /notice %}}

![Visual Studio Code](/images/1.Setup/Setup11.png?width=90pc)
![Visual Studio Code](/images/1.Setup/Setup12.png?width=90pc)

{{% notice note %}}
tạo thư mục mới cho dự án của chúng ta, hãy đặt tên: "mycdkproject"
{{% /notice %}}

![Visual Studio Code](/images/1.Setup/Setup13.png?width=90pc)
{{% notice tip %}}
Đảm bảo bạn đang ở thư mục gốc của dự án:
{{% /notice %}}
````
mkdir mycdkproject
````

Chọn: "Open Folder"
![Visual Studio Code](/images/1.Setup/Setup14.png?width=90pc)

chọn đích đến và đặt tên thư mục "mycdkproject" và nhấp vào "Select Folder"
![Visual Studio Code](/images/1.Setup/Setup15.png?width=90pc)

Bạn sẽ mở một cửa sổ mới có "MYCDKPRJECT" ở panel bên trái
![Visual Studio Code](/images/1.Setup/Setup16.png?width=90pc)