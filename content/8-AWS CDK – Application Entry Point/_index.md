---
title : "AWS CDK – Application Entry Point"
date :  "`r Sys.Date()`" 
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---
Make sure your app.py look like this:

![CDK](/images/8.AWS_CDK–Application_Entry_Point/AWS_CDK–Application_Entry_Point1.png?width=40pc)

Then we will code like this:
````
#!/usr/bin/env python3
import os

import aws_cdk as cdk
from aws_cdk import Tags
from decouple import config

from bucket_deployment_stack.bucket_deployment_stack import BucketDeploymentStack
from emr_cluster_stack.emr_cluster_stack import EMRClusterStack
from security_stack.security_stack import SecurityStack

# Set global variables
ID = config('id')
PRIMARY_BUCKET = f"emr-pipeline-{ID}"
LOG_BUCKET = f"emr-logs-{ID}"
SCRIPT_LOCATION = f"{PRIMARY_BUCKET}/scripts/"
VPC_NAME = f"emr-pipeline-vpc-{ID}"

env_USA = cdk.Environment(account="707843606607", region="ap-southeast-1")  #Change this
app = cdk.App()

# Create Stacks
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


# Add dependencies
emr_cluster_stack.add_dependency(bucket_deployment_stack)
emr_cluster_stack.add_dependency(security_stack)


# Add tags
Tags.of(app).add("ProjectOwner", "hktafk")          #Change this
Tags.of(app).add("Project", "EMR-ETL-Pipeline")     #Change this

app.synth()
````

{{% notice warning %}}
You'll have to change `account id` and `region`
{{% /notice %}}

{{% notice tip %}}
account=["your AWS account number"] 
{{% /notice %}}

{{% notice tip %}}
It is best practice to have tags. So change `ProjectOwner` and `Project` tags.
{{% /notice %}}