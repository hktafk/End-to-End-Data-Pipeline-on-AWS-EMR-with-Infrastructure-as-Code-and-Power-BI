---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1. </b> "
---
### Quy trình hoàn chỉnh xây dựng Data Pipeline từ đầu đến cuối trên AWS EMR với AWS CDK, IaC và trực quan hóa bằng Power BI

#### Tổng quan
 Trong bài thực hành này, bạn sẽ học cách xây dựng ETL Pipeline trên Amazon EMR với IaC (Infrastructure as code), AWS CDK và Apache Hive. Bạn sẽ triển khai pipeline sử dụng S3, Visual Studio Code, và AWS EMR, sau đó sử dụng Power BI để tạo các biểu đồ trực quan hóa dữ liệu từ dữ liệu đã được chuyển đổi.

#### Kiến trúc Dự án
![Architechture](/images/1.Setup/Setup0.png?)

#### Tổng quan về vấn đề doanh nghiệp:
 Infrastructure as Code (IaC) là một phương pháp tự động hóa việc cung cấp và quản lý hạ tầng CNTT bằng các kỹ thuật kỹ thuật phần mềm. Nó bao gồm việc tạo và duy trì hạ tầng thông qua mã thay vì cấu hình thủ công từng thành phần riêng lẻ.

IaC thường được sử dụng trong môi trường điện toán đám mây, nơi nó cho phép các nhà phát triển và nhóm vận hành tự động hóa việc triển khai và quản lý tài nguyên, chẳng hạn như máy chủ, lưu trữ và mạng. Nó cho phép các tổ chức đạt được hạ tầng nhất quán, đáng tin cậy và có thể mở rộng hơn, có thể dễ dàng sao chép trên nhiều môi trường. IaC có thể được triển khai bằng các công cụ và nền tảng khác nhau, chẳng hạn như Terraform, AWS CloudFormation, Azure Resource Manager và Google Cloud Deployment Manager.

Các công cụ này cho phép tạo các mẫu hoặc tập lệnh hạ tầng xác định cấu hình và trạng thái mong muốn của hạ tầng.

Lợi ích của IaC bao gồm tăng tốc độ và sự nhanh nhẹn của việc triển khai hạ tầng, cải thiện tính nhất quán và độ tin cậy của hạ tầng, giảm lỗi thủ công và chi phí, và tăng cường hợp tác giữa các nhóm phát triển và vận hành.

#### Infrastructure as Code (IaC) là nhu cầu cấp thiết vì nhiều lý do:

- Hạ tầng thay đổi nhanh chóng: Trong môi trường kỹ thuật số phát triển nhanh ngày nay, hạ tầng cần phải nhanh nhẹn và đáp ứng với nhu cầu kinh doanh thay đổi. IaC cho phép cung cấp, cập nhật và mở rộng hạ tầng nhanh chóng và hiệu quả, điều này rất cần thiết để đáp ứng nhu cầu kinh doanh.
- Tự động hóa: IaC tự động hóa quá trình triển khai và quản lý hạ tầng, giảm khả năng xảy ra lỗi của con người và cải thiện hiệu quả tổng thể. Nó cũng cho phép triển khai nhanh hơn và đáng tin cậy hơn, có thể dẫn đến tăng năng suất và giảm chi phí.
- Tính nhất quán: IaC đảm bảo rằng hạ tầng được cấu hình nhất quán trên các môi trường khác nhau, giảm nguy cơ lệch cấu hình và cải thiện độ tin cậy tổng thể của hệ thống.
- Hợp tác: IaC khuyến khích sự hợp tác giữa các nhóm phát triển và vận hành bằng cách cho phép họ làm việc cùng nhau trên mã hạ tầng. Điều này có thể dẫn đến giao tiếp tốt hơn, giải quyết vấn đề nhanh hơn và cải thiện sự phối hợp giữa các nhóm khác nhau.
- Tuân thủ: IaC có thể giúp các tổ chức duy trì tuân thủ các tiêu chuẩn và quy định của ngành bằng cách cung cấp một cách tiếp cận nhất quán và có thể kiểm toán đối với quản lý hạ tầng.

#### AWS Cloud Development Kit (CDK):

AWS Cloud Development Kit (CDK) là một framework phát triển phần mềm cho phép các nhà phát triển định nghĩa hạ tầng đám mây bằng các ngôn ngữ lập trình quen thuộc như TypeScript, Python, Java và .NET. Nó cung cấp một abstraction hướng đối tượng cấp cao hơn trên AWS CloudFormation, cho phép mã hiệu quả và biểu cảm hơn.

Infrastructure as Code (IaC) sử dụng AWS Cloud Development Kit (CDK) là một cách định nghĩa và triển khai tài nguyên AWS bằng mã. AWS CDK cho phép các nhà phát triển định nghĩa hạ tầng đám mây bằng các ngôn ngữ lập trình quen thuộc như TypeScript, Python, Java và .NET, sử dụng các cấu trúc hướng đối tượng và abstraction cấp cao. Một số lợi ích của việc sử dụng AWS CDK cho IaC bao gồm Ngôn ngữ lập trình quen thuộc, Abstraction hướng đối tượng cấp cao, Tính nhất quán và khả năng bảo trì, và khả năng tương thích với AWS CloudFormation.

#### Mục tiêu:
Mục tiêu của dự án này là xây dựng ETL Pipeline trên Amazon EMR thông qua AWS CDK. Pipeline sẽ bao gồm việc thực hiện phân tích và chuyển đổi dữ liệu bằng Apache Hive trên EMR. Ngoài ra, chúng ta sẽ tạo một dashboard tương tác trên Power BI để trực quan hóa kết quả.

- Hiểu về bộ dữ liệu Sales
- Hiểu về AWS CDK
- Cài đặt AWS CDK và các lệnh khác nhau của nó
- Ưu điểm của công nghệ Serverless
- Sự khác biệt giữa UUID và NanoID
- Sự khác biệt giữa Hive và Spark
- Hiểu về S3 Bucket deployment stack
- Hiểu về Security stack
- Hiểu về Hive script để tạo bảng
- Hiểu về Hive script để chuyển đổi dữ liệu
- Hiểu về EMR cluster stack
- Triển khai AWS CDK stacks
- Debug AWS CDK stacks
- Kết nối với bảng Hive bằng Power BI
- Tạo trực quan hóa bằng Power BI

#### Tech Stack:
- Ngôn ngữ: Python
- Dịch vụ: AWS S3, Visual Code Studio, AWS CDK, AWS EMR, Power BI, Apache Hive