---
title : "Deploy EMR Cluster Stack"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 9.3 </b> "
---
Run this first to create role:

````
aws emr create-default-roles
````
![Deploy EMR Cluster Stack](/images/9.AWS_CDK_–_Deploying_Stacks/9.3.Deploy_EMR_Cluster_Stack/Deploy_EMR_Cluster_Stack1.png?width=40pc)

````
cdk synth EMRClusterStack 
````
![Deploy EMR Cluster Stack](/images/9.AWS_CDK_–_Deploying_Stacks/9.3.Deploy_EMR_Cluster_Stack/Deploy_EMR_Cluster_Stack2.png)

Then you can deploy : 
{{% notice note %}}
This could took 5-10 minutes, be patient!
{{% /notice %}}

````
cdk deploy EMRClusterStack
````

![Deploy EMR Cluster Stack](/images/9.AWS_CDK_–_Deploying_Stacks/9.3.Deploy_EMR_Cluster_Stack/Deploy_EMR_Cluster_Stack3.png?width=90pc)

