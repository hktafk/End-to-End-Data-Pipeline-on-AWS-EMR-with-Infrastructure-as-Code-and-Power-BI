---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 14
chapter : false
pre : " <b> 14. </b> "
---

Trong bước cuối cùng này, chúng ta sẽ dọn dẹp tất cả tài nguyên AWS được tạo trong workshop này để tránh các khoản phí liên tục.

{{% notice warning %}}
Đảm bảo thực hiện các bước này theo thứ tự để hoàn toàn xóa tất cả tài nguyên và tránh các khoản phí không mong muốn.
{{% /notice %}}

## Bước 1: Terminate EMR Cluster

Đầu tiên, chúng ta cần terminate EMR cluster vì đây là tài nguyên tốn kém nhất.

1. Vào **AWS EMR Console**
2. Chọn EMR cluster của bạn
3. Nhấp **Terminate**
4. Xác nhận terminate

![Terminate EMR Cluster](/images/14.Clean_up_resources/Clean_up_resources1.png)

{{% notice tip %}}
Thay đổi region của bạn về nơi bạn lưu EMR Cluster
{{% /notice %}}

![Terminate EMR Cluster](/images/14.Clean_up_resources/Clean_up_resources2.png)

![Terminate EMR Cluster](/images/14.Clean_up_resources/Clean_up_resources3.png)

{{% notice note %}}
Đợi EMR cluster terminate hoàn toàn trước khi tiến hành bước tiếp theo.
{{% /notice %}}

## Bước 2: Dọn dẹp VPC Resources
Vào VPC Console
1. Vào **AWS VPC Console**
2. Xóa VPC được tạo cho dự án này
{{% notice tip %}}
Của tôi là `vpc-0c17b843293d26a07` nhưng VPC của bạn có thể trông khác
{{% /notice %}}
1. Điều này sẽ tự động dọn dẹp:
   - Subnets
   - Security Groups
   - Route Tables
   - Internet Gateway

![Delete VPC](/images/14.Clean_up_resources/Clean_up_resources8.png)

## Bước 3: Xóa CDK Stacks

Sử dụng AWS CDK để destroy tất cả các stack chúng ta đã tạo:

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
Gõ 'y' khi được nhắc để xác nhận xóa từng stack.
{{% /notice %}}

## Bước 4: Xác minh Xóa CloudFormation Stacks

1. Vào **AWS CloudFormation Console**
2. Kiểm tra tất cả stack đã được xóa hoặc ở trạng thái **DELETE_COMPLETE**
3. Nếu có stack nào bị kẹt, xóa thủ công

![CloudFormation Cleanup](/images/14.Clean_up_resources/Clean_up_resources9.png)

## Bước 5: Dọn dẹp S3 Buckets

1. Vào **AWS S3 Console**
2. Xóa primary bucket: `emr-pipeline-[nanoid-của-bạn]`
3. Xóa log bucket: `emr-logs-[nanoid-của-bạn]`
4. Xóa CDK bootstrap bucket: `cdk-hnb659fds-assets-[account-id]-[region]`

![Delete S3 Buckets](/images/14.Clean_up_resources/Clean_up_resources10.png)

{{% notice warning %}}
Đảm bảo làm trống bucket trước khi xóa chúng.
{{% /notice %}}
![Delete S3 Buckets](/images/14.Clean_up_resources/Clean_up_resources11.png)

## Bước 6: Xóa IAM Roles (nếu cần)

1. Vào **AWS IAM Console**
2. Kiểm tra các role liên quan đến EMR còn lại
3. Xóa các role được tạo cho dự án này:
   - `EMR_EC2_DefaultRole`
   - `EMR_DefaultRole`
   - Bất kỳ role tùy chỉnh nào được tạo bởi EMR mà bạn biết là không cần thiết

![Delete IAM Roles](/images/14.Clean_up_resources/Clean_up_resources12.png)

## Bước 7: Xóa Key Pairs

1. Vào **AWS EC2 Console**
2. Điều hướng đến **Key Pairs**
3. Xóa key pair được sử dụng để truy cập EMR cluster

![Delete Key Pairs](/images/14.Clean_up_resources/Clean_up_resources13.png)

## Bước 8: Xác minh Tất cả Tài nguyên đã được Xóa

Kiểm tra các dịch vụ AWS sau để đảm bảo không còn tài nguyên nào:

1. **EMR**: Không có cluster đang hoạt động
2. **EC2**: Không có instance đang chạy
3. **S3**: Không có bucket liên quan đến dự án
4. **VPC**: Không có VPC tùy chỉnh
5. **IAM**: Không có role cụ thể của dự án
6. **CloudFormation**: Không có stack đang hoạt động

## Bước 9: Kiểm tra AWS Billing

1. Vào **AWS Billing Console**
2. Xem lại các khoản phí hiện tại
3. Thiết lập cảnh báo billing nếu chưa được cấu hình
4. Theo dõi các khoản phí không mong muốn trong vài ngày tới

{{% notice info %}}
Đừng lo lắng, chi phí của bạn sẽ không cao như vậy. Điều này là do tôi đã để dự án vài ngày nên nó tính phí tôi nhiều như vậy.
{{% /notice %}}

![Check Billing](/images/14.Clean_up_resources/Clean_up_resources14.png)

{{% notice info %}}
Có thể mất đến 24 giờ để tất cả các khoản phí ngừng xuất hiện trong dashboard billing của bạn.
{{% /notice %}}

## Tóm tắt Lệnh Cleanup

Để tham khảo nhanh, đây là tất cả các lệnh cleanup:

````bash
# Destroy CDK stacks
cdk destroy EMRClusterStack
cdk destroy BucketDeploymentStack  
cdk destroy SecurityStack

# Xác minh xóa stack
aws cloudformation list-stacks --stack-status-filter DELETE_COMPLETE

# Liệt kê S3 bucket còn lại
aws s3 ls
````

{{% notice success %}}
Chúc mừng! Bạn đã hoàn thành thành công workshop và dọn dẹp tất cả tài nguyên AWS. Tài khoản AWS của bạn sẽ không còn phát sinh phí từ dự án này.
{{% /notice %}}

## Khắc phục sự cố

Nếu bạn gặp vấn đề trong quá trình cleanup:

1. **Xóa stack thất bại**: Kiểm tra dependencies và xóa tài nguyên thủ công
2. **S3 bucket không thể xóa**: Đảm bảo bucket hoàn toàn trống
3. **EMR cluster không thể terminate**: Force terminate từ console
4. **Phí billing tiếp tục**: Liên hệ AWS support nếu phí vẫn tiếp tục sau 48 giờ

![Troubleshooting](/images/14.Clean_up_resources/we-did-it-celebration-meme.jpg?width=50pc)