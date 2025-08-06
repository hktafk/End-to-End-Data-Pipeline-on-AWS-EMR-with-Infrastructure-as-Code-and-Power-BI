---
title : "AWS CDK – Deploying Stacks"
date :  "`r Sys.Date()`" 
weight : 9
chapter : false
pre : " <b> 9 </b> "
---
Now type : 

````
ls
````
{{% notice tip %}}
Make sure you’re in the same directory as `cdk.json` (cdk command will fail if not)
{{% /notice %}}


{{% notice note %}}
`cd ..` for going back the previous directory
{{% /notice %}}

![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks1.png)


Now type:
````
cdk synth  BucketDeploymentStack
````
![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks2.png)

We have synthesizing the deployment stack but it still hasn’t developed yet, to do  that we’ll type:

````
cdk deploy BucketDeploymentStack
````

{{% notice tip %}}
If ask for deploy changes just press `y` (yes).
{{% /notice %}}
![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks3.png)

If it successfully deployed, the result should be like this:
![CDK](/images/9.AWS_CDK_–_Deploying_Stacks/AWS_CDK–Deploying_Stacks4.png)

{{% notice tip %}}
You could use to upgrade cdk to latest version:
````
npm install -g aws-cdk
````
{{% /notice %}}

