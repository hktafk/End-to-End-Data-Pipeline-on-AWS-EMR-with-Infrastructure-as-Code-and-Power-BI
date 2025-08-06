---
title : "Create AWS S3 Bucket Deployment stack"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
{{% notice tip %}}
Make sure you are in the root directory of your project:
{{% /notice %}}
````
mkdir bucket_deployment_stack
cd bucket_deployment_stack  
code bucket_deployment_stack.py
````

code for bucket_deployment_stack.py:
````
from aws_cdk import (
    Stack,
    aws_s3_deployment as s3deploy,
    aws_s3 as s3,
)
from constructs import Construct
from decouple import config

# Deploys data to S3 which triggers the lambda
class BucketDeploymentStack(Stack):

    def __init__(self,
                 scope: Construct, 
                 construct_id: str,
                 primary_bucket_name: str,
                 log_bucket_name: str,
                 **kwargs
                ) -> None:
        super().__init__(scope, construct_id, **kwargs)

        primary_bucket = s3.Bucket(
            self,
            id=primary_bucket_name,
            bucket_name=log_bucket_name
        )
 
        log_bucket = s3.Bucket(
            self,
            id=log_bucket,
            bucket_name=log_bucket
        )
    
        data_deployment = s3deploy.BucketDeployment(self, "DeployData",
                sources=[s3deploy.Source.asset("./emr_pipeline/")],
                destination_bucket=primary_bucket,
                destination_key_prefix="emr_pipeline/",
                prune=False
            )

````