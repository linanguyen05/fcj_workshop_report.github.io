---
title: "Worklog Tuần 4"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Triển khai thành công Auto Scaling Group (ASG) kết hợp Application Load Balancer (ALB), làm chủ chiến lược Predictive Scaling để dự báo tải chủ động.
* Xây dựng hệ thống giám sát toàn diện với CloudWatch, tận dụng Logs Insights và Math Expressions để truy vết lỗi và phân tích hiệu năng chuyên sâu.
* Nắm vững thiết kế NoSQL với DynamoDB (ưu tiên Query/GSI, hạn chế Scan) và thiết lập mô hình DNS Hybrid kết nối On-premise qua Route 53 Resolver.
* Chuyển dịch thao tác từ Console sang AWS CLI v2, hiểu rõ cách tương tác trực tiếp với API để quản lý tài nguyên (VPC, S3, IAM) hiệu quả.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | **CHỦ ĐỀ: TRIỂN KHAI ỨNG DỤNG HIGH AVAILABILITY VỚI ASG & ELB** <br>- **Lý thuyết:** <br>  + Hiểu cơ chế hoạt động của Amazon EC2 Auto Scaling (ASG) và Application Load Balancer (ALB). <br>  + Phân tích các chiến lược Scaling: Manual, Scheduled, Dynamic và đặc biệt là Predictive Scaling (dùng ML để dự đoán tải). <br>  + Kiến trúc Multi-AZ cho RDS Database và Security Group. <br>- **Thực hành:** <br>  + Setup hạ tầng: Tạo VPC, khởi tạo RDS MySQL (Multi-AZ) và cài đặt môi trường Node.js trên EC2. <br>  + Cấu hình Scaling: Tạo AMI, Launch Template và thiết lập Target Group cho ALB. <br>  + Kiểm thử chịu tải: Sử dụng công cụ Stress Tool để kiểm chứng khả năng tự động Scale-out/Scale-in của hệ thống qua các kịch bản Dynamic và Predictive Scaling. | 29/09/2025 | 29/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | **CHỦ ĐỀ: GIÁM SÁT & VẬN HÀNH HỆ THỐNG VỚI AMAZON CLOUDWATCH** <br>- **Lý thuyết:** <br>  + Nắm được 4 thành phần cốt lõi: Metrics (số liệu), Logs (nhật ký), Alarms (cảnh báo) và Dashboards (bảng điều khiển). <br>  + Các Best Practices về đặt tên và tối ưu chi phí lưu trữ Logs (Retention settings). <br>- **Thực hành:** <br>  + Metrics & Math: Tùy chỉnh biểu đồ metrics, sử dụng Math Expressions (Search/Sort) để phân tích dữ liệu CPU/Disk. <br>  + Logs Insights: Cấu hình Retention cho logs và viết truy vấn để lọc lỗi (ERROR/WARN) từ ứng dụng. <br>  + Alarms & Dashboard: Thiết lập Metric Filter, tạo Alarm gửi cảnh báo qua SNS và tổng hợp widget lên Dashboard giám sát tập trung. | 30/09/2025 | 30/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | **CHỦ ĐỀ: XÂY DỰNG HỆ THỐNG HYBRID DNS VỚI ROUTE 53 RESOLVER** <br>- **Lý thuyết:** <br>  + Tổng quan mô hình DNS Hybrid kết nối giữa On-premise và AWS. <br>  + Cơ chế hoạt động của Route 53 Resolver: Inbound Endpoints (nhận query) và Outbound Endpoints (gửi query). <br>  + Tìm hiểu quy tắc chuyển tiếp (Resolver Rules). <br>- **Thực hành:** <br>  + Giả lập On-premise: Triển khai AWS Managed Microsoft AD và RD Gateway server thông qua CloudFormation. <br>  + Setup Resolver: Tạo Outbound Endpoint để đẩy query từ AWS về AD và Inbound Endpoint để nhận query ngược lại[cite: 40, 48]. <br>  + Kiểm thử: Sử dụng `nslookup` và `Resolve-DnsName` để xác nhận khả năng phân giải tên miền private giữa hai môi trường. | 01/10/2025 | 01/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | **CHỦ ĐỀ: QUẢN TRỊ CƠ SỞ DỮ LIỆU NOSQL VỚI AMAZON DYNAMODB** <br>- **Lý thuyết:** <br>  + Kiến trúc DynamoDB: Table, Items, Attributes và các loại Primary Key (Partition vs Composite). <br>  + Phân biệt Scan (quét toàn bộ) vs Query (truy vấn theo key) và Global Secondary Index (GSI). <br>  + Các mô hình nhất quán: Eventually Consistent vs Strongly Consistent Reads. <br>- **Thực hành:** <br>  + Console & CLI: Tạo bảng Music/Movies, thực hiện CRUD (thêm/xóa/sửa) items trực tiếp trên Console và qua AWS CloudShell. <br>  + AWS SDK (Boto3): Viết script Python để tương tác với DB như Load dữ liệu hàng loạt, Query theo Index và Scan với bộ lọc. <br>  + Tối ưu: Thực hành tạo GSI để tăng tốc độ truy vấn thay vì dùng Scan. | 02/10/2025 | 02/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | **CHỦ ĐỀ: TỰ ĐỘNG HÓA & QUẢN TRỊ HẠ TẦNG BẰNG AWS CLI** <br>- **Lý thuyết:** <br>  + Lợi ích của AWS CLI v2 trong việc tự động hóa và tương tác trực tiếp với API. <br>  + Cấu hình Profile, Region, Output format (JSON/Table/Text) và bảo mật Access Key. <br>- **Thực hành:** <br>  + Cấu hình môi trường: Cài đặt AWS CLI v2, setup profile mặc định và named profile. <br>  + Quản trị dịch vụ: Sử dụng lệnh CLI để quản lý S3 (tạo bucket), SNS (pub/sub), và IAM (tạo User/Group). <br>  + Dựng VPC & EC2: Thực hiện chuỗi lệnh tạo VPC, Subnet, IGW, Route Table và khởi chạy EC2 Instance hoàn toàn bằng dòng lệnh. | 03/10/2025 | 03/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) 

### Kết quả đạt được tuần 4:

  * **Chuyển đổi tư duy Scaling:** Làm chủ việc chuyển đổi mô hình từ Thụ động (Reactive - Dynamic Scaling) sang Chủ động (Proactive - Predictive Scaling), giúp hệ thống tự động chuẩn bị tài nguyên trước thời điểm tải cao điểm.
  * **Giám sát có chiều sâu (Observability):** Không chỉ dừng lại ở xem metrics cơ bản, đã vận dụng thành thạo Logs Insights để truy vết lỗi (ERROR logs) và Math Expressions để phân tích dữ liệu tùy chỉnh.
  * **Tối ưu hóa NoSQL:** Hiểu sâu sắc về Access Patterns trong DynamoDB, phân biệt rõ ràng hiệu năng giữa Scan và Query, từ đó áp dụng Global Secondary Index (GSI) để tối ưu hóa truy vấn.
  * **Kết nối Hybrid & Tự động hóa:** Triển khai thành công mô hình mạng lai (Hybrid DNS) với Route 53 Resolver và thành thạo thao tác quản trị hạ tầng qua AWS CLI thay vì chỉ phụ thuộc vào Console.

### Khó khăn – Giải pháp:

  * **Hiệu suất DynamoDB:** Khó khăn trong việc phân biệt khi nào dùng Scan và Query, lo ngại tiêu tốn Read Capacity Units (RCU) khi dữ liệu lớn.

      * **Giải pháp:** Áp dụng chiến lược "Query First". Sử dụng Global Secondary Index (GSI) để tạo các góc nhìn dữ liệu khác nhau, cho phép dùng lệnh Query thay vì Scan toàn bảng.

  * **Predictive Scaling không hoạt động ngay:** Khi mới cấu hình, ASG không dự đoán được tải do thiếu dữ liệu lịch sử (cần ít nhất 2 ngày).

      * **Giải pháp:** Thực hiện script giả lập dữ liệu lịch sử và nạp Custom Metrics vào CloudWatch để "dạy" cho mô hình Machine Learning của AWS hiểu pattern của hệ thống.

  * **Thao tác với AWS CLI:** Output trả về dạng JSON quá dài và khó đọc, khó lấy được ID của tài nguyên vừa tạo để dùng cho lệnh tiếp theo.

      * **Giải pháp:** Sử dụng tham số `--query` để lọc chính xác trường dữ liệu cần thiết và `--output text/table` để hiển thị kết quả trực quan, dễ dàng tái sử dụng trong script.

### Bài học rút ra:

  * Trong môi trường Cloud, khả năng dự đoán (predictability) là chìa khóa để cân bằng giữa Hiệu năng và Chi phí. Predictive Scaling giúp ta chuẩn bị trước thay vì chỉ chạy theo sự cố.

  * Thu thập Logs và Metrics chỉ có giá trị khi nó kích hoạt một hành động cụ thể (Alarms, Auto Scaling) hoặc giúp trả lời câu hỏi "Tại sao?" nhanh chóng (Logs Insights). Nếu không, đó chỉ là lãng phí chi phí lưu trữ.

  * Khác với SQL, với DynamoDB ta phải xác định Access Patterns trước khi thiết kế bảng. Việc chọn sai Primary Key hoặc Index ngay từ đầu sẽ dẫn đến những hệ quả lớn về hiệu năng và chi phí sau này.