---
title : "AWS CDK – Deploying Stacks"
date :  "`r Sys.Date()`" 
weight : 9
chapter : false
pre : " <b> 9 </b> "
---
Bây giờ gõ: 

````
ls
````
{{% notice tip %}}
Đảm bảo bạn đang ở cùng thư mục với `cdk.json` (lệnh cdk sẽ thất bại nếu không)
{{% /notice %}}


{{% notice note %}}
`cd ..` để quay về thư mục trước
{{% /notice %}}

![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks1.png)


Bây giờ gõ:
````
cdk synth  BucketDeploymentStack
````
![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks2.png)

Chúng ta đã synthesizing deployment stack nhưng nó vẫn chưa được phát triển, để làm điều đó chúng ta sẽ gõ:

````
cdk deploy BucketDeploymentStack
````

{{% notice tip %}}
Nếu hỏi về deploy changes chỉ cần nhấn `y` (yes).
{{% /notice %}}
![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks3.png)

Nếu nó được triển khai thành công, kết quả sẽ như thế này:
![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks4.png)

{{% notice tip %}}
Bạn có thể sử dụng để nâng cấp cdk lên phiên bản mới nhất:
````
npm install -g aws-cdk
````
{{% /notice %}}