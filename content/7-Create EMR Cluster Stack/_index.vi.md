---
title : "Tạo EMR Cluster Stack"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
#### 1. Trong module này, chúng ta sẽ:
- Tạo thư mục mới
- Tạo file python mới
- Tạo class EMR cluster stack mới

Bên trong class mới:
+ Tạo policy mới để đọc từ thư mục scripts
+ Tạo EMR Cluster
+ Lấy subnet ID chính xác từ AWS console dưới EC2-VPC
+ Tạo Hive step để tạo bảng
+ Tạo Hive step để chuyển đổi dữ liệu


````
# Tạo thư mục mới  
mkdir emr_cluster_stack 
# Tạo file python mới và code
code emr_cluster_stack/emr_cluster_stack.py
````
#### emr_cluster_stack.py
````
from aws_cdk import aws_ec2 as ec2, aws_iam as iam, App, Aws, Stack, aws_emr as emr
from constructs import Construct

MASTER_INSTANCE_TYPE = "m5.xlarge"
CORE_INSTANCE_TYPE = "m5.xlarge"
CORE_INSTANCE_COUNT = 2
MARKET = "ON_DEMAND"
CLUSTER_NAME = "emr-pipeline-cluster"
EMR_RELEASE="emr-6.10.0"
SUBNET_ID ="subnet-0b73564c58134f5ae"

class EMRClusterStack(Stack):
    def __init__(
        self,
        scope: Construct,
        id: str,
        s3_log_bucket: str,
        s3_script_bucket: str,
        vpc_name: str,
        **kwargs,
    ) -> None:
        super().__init__(scope, id, **kwargs)

        scripts_location = f"{s3_script_bucket}/emr_pipeline/scripts"

        # cho phép đọc scripts từ s3 bucket
        read_scripts_policy = iam.PolicyStatement(
            effect=iam.Effect.ALLOW,
            actions=["s3:GetObject",],
            resources=[f"arn:aws:s3:::{scripts_location}/*"],
        )
        read_scripts_document = iam.PolicyDocument()
        read_scripts_document.add_statements(read_scripts_policy)

        # emr service role
        emr_service_role = iam.Role(
            self,
            "emr_service_role",
            assumed_by=iam.ServicePrincipal("elasticmapreduce.amazonaws.com"),
            managed_policies=[
                iam.ManagedPolicy.from_aws_managed_policy_name(
                    "service-role/AmazonElasticMapReduceRole"
                )
            ],
            inline_policies={
                "read_scripts_document": read_scripts_document
            },
        )

        # emr job flow role
        emr_job_flow_role = iam.Role(
            self,
            "emr_job_flow_role",
            assumed_by=iam.ServicePrincipal("ec2.amazonaws.com"),
            managed_policies=[
                iam.ManagedPolicy.from_aws_managed_policy_name(
                    "service-role/AmazonElasticMapReduceforEC2Role"
                )
            ],
        )
        # emr job flow profile
        emr_job_flow_profile = iam.CfnInstanceProfile(
            self,
            "emr_job_flow_profile",
            roles=["EMR_EC2_DefaultRole"],
            instance_profile_name="emrJobFlowProfile_",
        )

        # tạo emr cluster
        emr_cluster = emr.CfnCluster(
            self,
            "emr_cluster",
            instances=emr.CfnCluster.JobFlowInstancesConfigProperty(
                core_instance_group=emr.CfnCluster.InstanceGroupConfigProperty(
                    instance_count=CORE_INSTANCE_COUNT,
                    instance_type=CORE_INSTANCE_TYPE,
                    market=MARKET
                ),
                ec2_subnet_id=SUBNET_ID,
                ec2_key_name="ProjectProAlexClark",             #Thay đổi cái này 
                keep_job_flow_alive_when_no_steps=True,
                master_instance_group=emr.CfnCluster.InstanceGroupConfigProperty(
                    instance_count=1,
                    instance_type=MASTER_INSTANCE_TYPE,
                    market=MARKET
                ),
            ),
            steps=[
                {
                    "actionOnFailure": "CANCEL_AND_WAIT",
                    "hadoopJarStep": {
                        "jar": "command-runner.jar",
                        "args": [
                            "hive",
                            "-f",
                            f"s3://{scripts_location}/create_tables.hql",
                        ],
                    },
                    "name": "create_tables",
                },
                {
                    "actionOnFailure": "CANCEL_AND_WAIT",
                    "hadoopJarStep": {
                        "jar": "command-runner.jar",
                        "args": [
                            "hive",
                            "-f",
                            f"s3://{scripts_location}/transform_data.hql",
                        ],
                    },
                    "name": "transform_data",
                }
            ],
            job_flow_role="EMR_EC2_DefaultRole",
            name=CLUSTER_NAME,
            applications=[emr.CfnCluster.ApplicationProperty(name="Hive")],
            service_role=emr_service_role.role_name,
            configurations=[],
            log_uri=f"s3://{s3_log_bucket}/{Aws.REGION}/elasticmapreduce/",
            release_label=EMR_RELEASE,
            visible_to_all_users=False,
        )
````
{{% notice warning %}}
Bạn sẽ phải thay đổi `ec2_key_name`
{{% /notice %}}

{{% notice tip %}}
Lấy ec2_key_name tại ([Đây](https://ap-southeast-1.signin.aws.amazon.com/oauth?client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fec2-tb&code_challenge=geRjHw_8lHuRsSi9OnjuDPlXoFa3VSZaIzVoSHAKBZw&code_challenge_method=SHA-256&response_type=code&redirect_uri=https%3A%2F%2Fap-southeast-1.console.aws.amazon.com%2Fec2%2Fhome%3FhashArgs%3D%2523KeyPairs%253A%26isauthcode%3Dtrue%26oauthStart%3D1754381727210%26region%3Dap-southeast-1%26state%3DhashArgsFromTB_ap-southeast-1_d80e6ccb17638bc9))
{{% /notice %}}

![EMR](/images/7.Create%20EMR%20Cluster%20Stack/EMRClusterStack10.png?width=90pc)

Mã Python này sử dụng AWS Cloud Development Kit (CDK) để định nghĩa một Amazon EMR (Elastic MapReduce) cluster. Dưới đây là giải thích về các thành phần và chức năng của nó:

#### Tổng quan
Mã này tạo một EMR cluster stack với cấu hình cụ thể cho các loại instance, IAM role, và cài đặt để chạy Hive scripts.

#### Các thành phần chính
##### 1. Hằng số:
- Loại Instance: Định nghĩa các loại instance được sử dụng cho master và core node (m5.xlarge).
- Số lượng Core Instance: Đặt số lượng core instance thành 2.
- Loại Market: Chỉ định rằng các instance sẽ là on-demand.
- Tên Cluster và EMR Release: Đặt tên cluster và phiên bản EMR sử dụng.
- Subnet ID: Chỉ định subnet mà EMR cluster sẽ chạy.

##### 2. Class EMRClusterStack:
- Class này kế thừa từ Stack và đóng gói hạ tầng cho EMR cluster.

##### 3. Vị trí S3 Script:
- Xây dựng vị trí S3 nơi lưu trữ EMR scripts.

##### 4. IAM Policies:
- Read Scripts Policy: Cho phép EMR cluster đọc scripts từ S3 bucket được chỉ định.
- EMR Service Role: Định nghĩa role cho EMR assume, có managed policies cho EMR service access cùng với inline policy để truy cập S3 scripts.
- EMR Job Flow Role: Tạo role cho EC2 instances trong EMR cluster, cho phép chúng thực hiện các hoạt động cần thiết.

##### 5. Cấu hình EMR Cluster:
- Job Flow Instances Configuration: Chỉ định cấu hình instance cho EMR cluster, bao gồm master và core instance groups.
- Master và Core Instances: Master instance được cấu hình có 1 node, trong khi core instances được đặt thành 2 node.
- Key Pair: Sử dụng EC2 key pair được chỉ định cho SSH access.
- Job Flow Role: Sử dụng default EMR EC2 role cho job execution.

##### 6. Các bước thực thi:
Cluster sẽ chạy hai bước:
- Tạo Bảng: Thực thi Hive script để tạo bảng trong data warehouse.
- Chuyển đổi Dữ liệu: Thực thi Hive script khác để chuyển đổi dữ liệu.

##### 7. Thuộc tính Cluster:
- Applications: Chỉ định rằng cluster sẽ chạy Hive.
- Service Role: Liên kết EMR service role đã tạo trước đó.
- Logging: Cấu hình S3 logging cho EMR cluster.
- Visibility: Đặt cluster không hiển thị với tất cả người dùng.

#### Tóm tắt
Mã này thiết lập EMR cluster trong AWS sử dụng CDK, cấu hình các IAM role cần thiết, loại instance, và job steps cho xử lý dữ liệu. Cluster được thiết kế để chạy Hive scripts lưu trữ trong S3 bucket, cho phép chuyển đổi và phân tích dữ liệu.