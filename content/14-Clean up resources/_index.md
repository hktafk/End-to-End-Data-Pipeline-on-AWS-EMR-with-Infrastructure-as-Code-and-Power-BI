---
title : "Clean up resources"
date :  "`r Sys.Date()`" 
weight : 14
chapter : false
pre : " <b> 14. </b> "
---

In this final step, we will clean up all AWS resources created during this workshop to avoid ongoing charges.

{{% notice warning %}}
Make sure to follow these steps in order to completely remove all resources and avoid unexpected charges.
{{% /notice %}}

## Step 1: Terminate EMR Cluster

First, we need to terminate the EMR cluster as it's the most expensive resource.

1. Go to **AWS EMR Console**
2. Select your EMR cluster
3. Click **Terminate**
4. Confirm termination

![Terminate EMR Cluster](/images/14.Clean_up_resources/Clean_up_resources1.png)

{{% notice tip %}}
Change your region to where you save EMR Cluster
{{% /notice %}}

![Terminate EMR Cluster](/images/14.Clean_up_resources/Clean_up_resources2.png)


![Terminate EMR Cluster](/images/14.Clean_up_resources/Clean_up_resources3.png)

{{% notice note %}}
Wait for the EMR cluster to fully terminate before proceeding to the next step.
{{% /notice %}}
## Step 2: Clean up VPC Resources
Go to VPC Console
1. Go to **AWS VPC Console**
2. Delete the VPC created for this project 
{{% notice tip %}}
Mine is `vpc-0c17b843293d26a07` but your VPC may look different
{{% /notice %}}
1. This will automatically clean up:
   - Subnets
   - Security Groups
   - Route Tables
   - Internet Gateway

![Delete VPC](/images/14.Clean_up_resources/Clean_up_resources8.png)


## Step 3: Delete CDK Stacks

Use AWS CDK to destroy all the stacks we created:

````
cdk destroy EMRClusterStack
````

![Destroy EMR Stack](/images/14.Clean_up_resources/Clean_up_resources4.png)
![Destroy EMR Stack](/images/14.Clean_up_resources/Clean_up_resources5.png)

````
cdk destroy BucketDeploymentStack
````

![Destroy Bucket Stack](/images/14.Clean_up_resources/Clean_up_resources6.png)

````
cdk destroy SecurityStack
````

![Destroy Security Stack](/images/14.Clean_up_resources/Clean_up_resources7.png)

{{% notice tip %}}
Type 'y' when prompted to confirm each stack deletion.
{{% /notice %}}

## Step 4: Verify CloudFormation Stacks Deletion

1. Go to **AWS CloudFormation Console**
2. Check that all stacks are deleted or in **DELETE_COMPLETE** status
3. If any stacks are stuck, manually delete them

![CloudFormation Cleanup](/images/14.Clean_up_resources/Clean_up_resources9.png)

## Step 5: Clean up S3 Buckets

1. Go to **AWS S3 Console**
2. Delete the primary bucket: `emr-pipeline-[your-nanoid]`
3. Delete the log bucket: `emr-logs-[your-nanoid]`
4. Delete the CDK bootstrap bucket: `cdk-hnb659fds-assets-[account-id]-[region]`

![Delete S3 Buckets](/images/14.Clean_up_resources/Clean_up_resources10.png)

{{% notice warning %}}
Make sure to empty the buckets before deleting them.
{{% /notice %}}
![Delete S3 Buckets](/images/14.Clean_up_resources/Clean_up_resources11.png)
## Step 6: Remove IAM Roles (if needed)

1. Go to **AWS IAM Console**
2. Check for any remaining EMR-related roles
3. Delete roles that were created for this project:
   - `EMR_EC2_DefaultRole`
   - `EMR_DefaultRole`
   - Any custom roles created by EMR that you'll know is unnecessary

![Delete IAM Roles](/images/14.Clean_up_resources/Clean_up_resources12.png)



## Step 7: Remove Key Pairs

1. Go to **AWS EC2 Console**
2. Navigate to **Key Pairs**
3. Delete the key pair used for EMR cluster access

![Delete Key Pairs](/images/14.Clean_up_resources/Clean_up_resources13.png)

## Step 8: Verify All Resources are Deleted

Check the following AWS services to ensure no resources remain:

1. **EMR**: No active clusters
2. **EC2**: No running instances
3. **S3**: No project-related buckets
4. **VPC**: No custom VPCs
5. **IAM**: No project-specific roles
6. **CloudFormation**: No active stacks



## Step 9: Check AWS Billing

1. Go to **AWS Billing Console**
2. Review current charges
3. Set up billing alerts if not already configured
4. Monitor for any unexpected charges over the next few days

{{% notice info %}}
Don't worry, your cost it's not gonna be this high. This is because i have left the project a few days so it charge me that much. 
{{% /notice %}}

![Check Billing](/images/14.Clean_up_resources/Clean_up_resources14.png)

{{% notice info %}}
It may take up to 24 hours for all charges to stop appearing in your billing dashboard.
{{% /notice %}}

## Cleanup Commands Summary

For quick reference, here are all the cleanup commands:

````bash
# Destroy CDK stacks
cdk destroy EMRClusterStack
cdk destroy BucketDeploymentStack  
cdk destroy SecurityStack

# Verify stack deletion
aws cloudformation list-stacks --stack-status-filter DELETE_COMPLETE

# List remaining S3 buckets
aws s3 ls
````

{{% notice success %}}
Congratulations! You have successfully completed the workshop and cleaned up all AWS resources. Your AWS account should no longer incur charges from this project.
{{% /notice %}}

## Troubleshooting

If you encounter issues during cleanup:

1. **Stack deletion fails**: Check dependencies and delete resources manually
2. **S3 bucket won't delete**: Ensure bucket is completely empty
3. **EMR cluster won't terminate**: Force terminate from console
4. **Billing charges continue**: Contact AWS support if charges persist after 48 hours

![Troubleshooting](/images/14.Clean_up_resources/we-did-it-celebration-meme.jpg?width=50pc)