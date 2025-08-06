---
title : "AWS CDK – Application Entry Point"
date :  "`r Sys.Date()`" 
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
Đảm bảo app.py của bạn trông như thế này:

![CDK](/images/8.AWS_CDK–Application_Entry_Point/AWS_CDK–Application_Entry_Point1.png?width=40pc)

Sau đó chúng ta sẽ code như thế này:
````
#!/usr/bin/env python3
import os

import aws_cdk as cdk
from aws_cdk import Tags
from decouple import config

from bucket_deployment_stack.bucket_deployment_stack import BucketDeploymentStack
from emr_cluster_stack.emr_cluster_stack import EMRClusterStack
from security_stack.security_stack import SecurityStack

# Đặt biến global
ID = config('id')
PRIMARY_BUCKET = f"emr-pipeline-{ID}"
LOG_BUCKET = f"emr-logs-{ID}"
SCRIPT_LOCATION = f"{PRIMARY_BUCKET}/scripts/"
VPC_NAME = f"emr-pipeline-vpc-{ID}"

env_USA = cdk.Environment(account="707843606607", region="ap-southeast-1")  #Thay đổi cái này
app = cdk.App()

# Tạo Stacks
security_stack = SecurityStack(
    scope=app,
    id="SecurityStack",
    vpc_name=VPC_NAME,
    env=env_USA
)


bucket_deployment_stack = BucketDeploymentStack(
    scope=app,
    construct_id=f"BucketDeploymentStack",
    primary_bucket_name=PRIMARY_BUCKET,
    log_bucket_name=LOG_BUCKET,
    env=env_USA
)


emr_cluster_stack = EMRClusterStack(
    scope=app,
    id=f"EMRClusterStack",
    s3_log_bucket=LOG_BUCKET,
    s3_script_bucket=PRIMARY_BUCKET,
    vpc_name=f"SecurityStack/{VPC_NAME}",
    env=env_USA
)


# Thêm dependencies
emr_cluster_stack.add_dependency(bucket_deployment_stack)
emr_cluster_stack.add_dependency(security_stack)


# Thêm tags
Tags.of(app).add("ProjectOwner", "hktafk")          #Thay đổi cái này
Tags.of(app).add("Project", "EMR-ETL-Pipeline")     #Thay đổi cái này

app.synth()
````

{{% notice warning %}}
Bạn sẽ phải thay đổi `account id` và `region`
{{% /notice %}}

{{% notice tip %}}
account=["số tài khoản AWS của bạn"] 
{{% /notice %}}

{{% notice tip %}}
Đây là best practice để có tags. Vì vậy hãy thay đổi tags `ProjectOwner` và `Project`.
{{% /notice %}}