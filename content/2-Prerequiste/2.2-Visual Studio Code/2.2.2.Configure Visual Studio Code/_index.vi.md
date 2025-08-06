---
title : "Cấu hình Visual Studio Code"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2.2 </b> "
---

![Visual Studio Code](/images/1.Setup/Setup16.png?width=90pc)

{{% notice tip %}}
Nhấp vào: View -> Terminal
{{% /notice %}}
![Visual Studio Code](/images/1.Setup/Setup17.png?width=90pc)

````
Python -m  pip install aws-cdk-lib
````
![Visual Studio Code](/images/1.Setup/Setup18.png?width=90pc)

````
cdk --version
````
![Visual Studio Code](/images/1.Setup/Setup19.png?width=90pc)

````
pip show aws-cdk-lib
````
![Visual Studio Code](/images/1.Setup/Setup20.png?width=90pc)

````
npm install -g aws-cdk
````
![Visual Studio Code](/images/1.Setup/Setup21.png?width=90pc)

````
cdk init --language python app
````
![Visual Studio Code](/images/1.Setup/Setup22.png?width=90pc)

````
cdk synth
````
![Visual Studio Code](/images/1.Setup/Setup23.png?width=90pc)

````
cdk bootstrap
````
![Visual Studio Code](/images/1.Setup/Setup24.png?width=90pc)

Kiểm tra S3 bucket:
![Visual Studio Code](/images/1.Setup/Setup250.png?width=90pc)

````
cdk diff
````
![Visual Studio Code](/images/1.Setup/Setup26.png?width=90pc)

````
cdk deploy
````
![Visual Studio Code](/images/1.Setup/Setup27.png?width=90pc)

Kiểm tra Cloudformation trên AWS Console:
![Visual Studio Code](/images/1.Setup/Setup281.png?width=90pc)

Cài đặt thư viện cần thiết:
![Visual Studio Code](/images/1.Setup/Setup29.png?width=90pc)

````
pip install -r requirements.txt 
````
![Visual Studio Code](/images/1.Setup/Setup30.png?width=90pc)