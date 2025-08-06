---
title : "AWS S3 Bucket Deployment stack "
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
#### Creating a bucket deployment stack:
- This containes all of AWS resources that have to do with creating bucket, storing data within S3.
- We have **primary bucket** for everything in this project.
- We have **log_bucket** (emr logs) which is best practice to do since you should store log separately from your main storage.	
- We have bucket deployment construct that taking all of the files within **emr_pipeline**      (which we we will create later) And uploading them to S3.


### Content:
<!--
   - [Update IAM Role](./4.1-updateiamrole/)
   - [Create **S3 Bucket**](./4.2-creates3bucket/)
   - [Create S3 Gateway endpoint](./4.3-creategwes3)
   - [Configure **Session logs**](./4.4-configsessionlogs/)
-->