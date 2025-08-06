---
title : "Mô tả Dữ liệu"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1.1. </b> "
---
#### Mô tả ngắn gọn
Chúng ta có một bộ dữ liệu ở đây mà chúng ta sẽ sử dụng để phân tích. Đây là dữ liệu bán hàng chung từ một công ty hoạt động trên toàn thế giới.

![AWS CLI](/images/DataDescription.png?width=90pc)

[Link để lấy data](https://github.com/hktafk/End-to-End-Data-Pipeline-on-AWS-EMR-with-Infrastructure-as-Code-AWS-CDK-and-Power-BI/blob/main/emr_pipeline/data/sales_data_raw/sales_data.csv)

{{% notice note %}}
Nhưng có điều gì đó quan trọng cần xem xét. Cả `order_date` và `ship date`, bạn sẽ nhận thấy dữ liệu có thể bị hỏng một chút (ví dụ: 10/18/2014, 11-07-2021). Chúng ta sẽ thực hiện chuyển đổi sau để sửa điều này.
{{% /notice %}}

#### 📊1. Tổng quan Bộ dữ liệu
Bộ dữ liệu này chứa 1.000 giao dịch bán hàng cá nhân được ghi lại từ ngày 1 tháng 1 năm 2010 đến ngày 26 tháng 7 năm 2017 cho một công ty hàng tiêu dùng toàn cầu. Nó nắm bắt thông tin chính về các sản phẩm được bán, thị trường địa lý, ngày đặt hàng/giao hàng, kênh bán hàng và các chỉ số tài chính (doanh thu, chi phí, lợi nhuận).

Các trường hợp sử dụng & Mục tiêu Kinh doanh:

- Phân tích Doanh thu & Lợi nhuận: Hiểu rõ khu vực, sản phẩm và kênh nào tạo ra nhiều doanh thu và lợi nhuận nhất.

- Tối ưu hóa Chuỗi cung ứng & Thời gian giao hàng: Đo lường độ trễ từ đặt hàng đến giao hàng và xác định cơ hội giảm thời gian thực hiện.

- Dự báo Nhu cầu & Lập kế hoạch Tồn kho: Phân tích các mẫu bán hàng lịch sử theo loại mặt hàng và khu vực để xây dựng mô hình dự đoán.

- Chiến lược Ưu tiên & Kênh: Đánh giá cách ưu tiên đơn hàng (ví dụ: "Cao" so với "Thấp") và kênh bán hàng (Trực tuyến so với Ngoại tuyến) tác động đến hiệu suất tổng thể.

#### 2. Yêu cầu Kinh doanh
Mục tiêu chính là thể hiện quy trình kỹ thuật dữ liệu và phân tích end-to-end:

- Thu thập & ETL
- Trích xuất CSV thô vào data lake
- Chuyển đổi ngày tháng, tính toán thời gian giao hàng và xác thực tính toán tài chính
- Tải dữ liệu đã làm sạch vào cơ sở dữ liệu quan hệ hoặc kho phân tích

- Phân tích & Trực quan hóa
- Xây dựng dashboard (Power BI, Tableau) để giám sát các chỉ số chính theo khu vực, sản phẩm, kênh và ưu tiên
- Triển khai truy vấn SQL và/hoặc script Python để tính toán trung bình trượt, tỷ lệ tăng trưởng và phát hiện ngoại lệ

- Mô hình Dự đoán
- Huấn luyện mô hình để dự báo khối lượng bán hàng và lợi nhuận hàng tháng theo danh mục sản phẩm và địa lý
- Đánh giá hiệu suất mô hình và tích hợp vào ứng dụng web đơn giản (Flask + Electron) cho người dùng kinh doanh

Bộ dữ liệu này cung cấp khả năng hiển thị đầy đủ về cả hiệu suất doanh thu (top-line) và lợi nhuận (bottom-line), cho phép thể hiện việc ra quyết định dựa trên dữ liệu.

#### 3. Định nghĩa Cột
Đây là schema được biểu diễn dưới dạng bảng Markdown:

| Cột                 | Kiểu    | Mô tả                                                                                  |
|---------------------|---------|----------------------------------------------------------------------------------------|
| **region**          | String  | Khu vực thế giới nơi đặt hàng. Ví dụ: "Asia", "Europe", "Sub-Saharan Africa".         |
| **country**         | String  | Quốc gia của khách hàng (tên ISO).                                                    |
| **item_type**       | String  | Danh mục sản phẩm được bán (ví dụ: "Fruits", "Cereal", "Cosmetics", "Baby Food").     |
| **sales_channel**   | String  | Kênh đặt hàng: **Online** hoặc **Offline**.                                           |
| **order_priority**  | String  | Ưu tiên của đơn hàng: **C** (Critical), **H** (High), **M** (Medium), **L** (Low).   |
| **order_date**      | Date    | Ngày đặt hàng. Định dạng `MM/DD/YYYY`.                                                |
| **order_id**        | Integer | Định danh duy nhất cho giao dịch bán hàng.                                            |
| **ship_date**       | Date    | Ngày giao hàng. Định dạng `MM-DD-YYYY`.                                               |
| **units_sold**      | Integer | Số lượng đơn vị được bán trong đơn hàng.                                              |
| **unit_price**      | Float   | Giá bán mỗi đơn vị (tính bằng USD).                                                   |
| **unit_cost**       | Float   | Chi phí mỗi đơn vị (tính bằng USD).                                                   |
| **total_revenue**   | Float   | Được tính là `units_sold × unit_price`.                                               |
| **total_cost**      | Float   | Được tính là `units_sold × unit_cost`.                                                |
| **total_profit**    | Float   | Được tính là `total_revenue − total_cost`.                                            |