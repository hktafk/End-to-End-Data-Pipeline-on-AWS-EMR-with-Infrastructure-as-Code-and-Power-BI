---
title : "Security Stack"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
#### Setting up security stack
This Stack will have all the security components for our AWS CDK project.

Check if you are on the right directory:
````
ls
````

{{% notice tip %}}
use ``cd ..`` if you want to go previous directory 
{{% /notice %}}   

{{% notice tip %}}
Make sure that you’re on the same directory as the `cdk.json`
{{% /notice %}}   

![Security Stack](/images/4.Security%20Stack/SecurityStack1.png?width=90pc)

````
mkdir security_stack
code security_stack/security_stack.py
````

Code for security_stack.py:
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

- Notice the “Stack” in `SecurityStack(Stack)`. That mean we define a class which is securityStack and we extend it with Stack library (Which we imported). So the class inherited the attribute of the Stack class.
- the `vpc_name: str` is the argument that we will use to create a VPC later on, which will be the VPC name that we’ll creating. 

{{% notice note %}}
`-> None` is just mean the function doesn’t return anything. Eg. If it was `-> int` or `-> str` it will return that type of value . This is optional , just a notation to make things clear.
{{% /notice %}}  

#### VPC Creation
VPC is Virtual Private Cloud. It offers a lot of security, so when the EMR Cluster run, it  will be running in this VPC, and nothing can access it , unless you have permission to do so (We will go over it later on)  
````
#VPC Creation
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
We have to set up a subnet_type and set to `PUBLIC` or else we won’t be able to access it from the internet.
{{% /notice %}}  


