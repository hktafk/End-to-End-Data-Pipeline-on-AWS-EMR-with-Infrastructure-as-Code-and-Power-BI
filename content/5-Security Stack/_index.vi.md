---
title : "Security Stack"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
#### Thiết lập security stack
Stack này sẽ có tất cả các thành phần bảo mật cho dự án AWS CDK của chúng ta.

Kiểm tra xem bạn có đang ở đúng thư mục không:
````
ls
````

{{% notice tip %}}
sử dụng ``cd ..`` nếu bạn muốn quay về thư mục trước 
{{% /notice %}}   

{{% notice tip %}}
Đảm bảo rằng bạn đang ở cùng thư mục với `cdk.json`
{{% /notice %}}   

![Security Stack](/images/4.Security%20Stack/SecurityStack1.png?width=90pc)

````
mkdir security_stack
code security_stack/security_stack.py
````

Code cho security_stack.py:
````
from aws_cdk import aws_ec2 as ec2, Stack
from constructs import Construct 

class SecurityStack(Stack):
    def __init__(
            self,
            scope: Construct,
            id: str,
            vpc_name: str,
            **kwargs,
    ) -> None:
        super().__init__(scope, id, **kwargs)

````

- Chú ý "Stack" trong `SecurityStack(Stack)`. Điều đó có nghĩa là chúng ta định nghĩa một class tên là securityStack và chúng ta mở rộng nó với thư viện Stack (mà chúng ta đã import). Vậy class này kế thừa thuộc tính của class Stack.
- `vpc_name: str` là tham số mà chúng ta sẽ sử dụng để tạo VPC sau này, đây sẽ là tên VPC mà chúng ta sẽ tạo. 

{{% notice note %}}
`-> None` chỉ có nghĩa là function không trả về gì. Ví dụ: Nếu là `-> int` hoặc `-> str` thì nó sẽ trả về kiểu giá trị đó. Điều này là tùy chọn, chỉ là một ký hiệu để làm rõ.
{{% /notice %}}  

#### Tạo VPC
VPC là Virtual Private Cloud. Nó cung cấp rất nhiều bảo mật, vì vậy khi EMR Cluster chạy, nó sẽ chạy trong VPC này, và không có gì có thể truy cập nó, trừ khi bạn có quyền để làm như vậy (Chúng ta sẽ đi qua điều này sau)  
````
#Tạo VPC
        vpc = ec2.Vpc(
            self,
            vpc_name,
            nat_gateways=0,
            subnet_configuration=[
                ec2.SubnetConfiguration(
                    name=vpc_name,
                    subnet_type=ec2.SubnetType.PUBLIC,
                )
            ]

        )

````
{{% notice note %}}
Chúng ta phải thiết lập subnet_type và đặt thành `PUBLIC` nếu không chúng ta sẽ không thể truy cập từ internet.
{{% /notice %}}  