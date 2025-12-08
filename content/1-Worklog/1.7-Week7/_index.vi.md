---
title: "Worklog Tuần 7"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
* **Ôn tập thi giữa kỳ (Mid-term Exam):** Vận dụng tổng hợp kiến thức về **Secure & Resilient Architectures** (IAM, VPC, Multi-AZ) và **Serverless** để hoàn thành xuất sắc bài đánh giá năng lực giai đoạn 1.
* **Nhập môn DevOps & CI/CD trên AWS:** Bắt đầu chuyển dịch từ triển khai thủ công sang tự động hóa. Nghiên cứu bộ công cụ **AWS Developer Tools** (CodeCommit, CodeBuild, CodePipeline) để xây dựng đường ống tích hợp và triển khai liên tục (Pipeline) cho ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | -------- | -------- | -------- | -------- |
| 2   | CHỦ ĐỀ: SERVERLESS ARCHITECTURE ON AWS <br>- Lý thuyết & Kiến trúc: <br>  + Hiểu mô hình Serverless, cơ chế "Pay-as-you-go" và vai trò của AWS Lambda kết hợp Amazon S3. <br>  + Phân tích luồng xử lý sự kiện (Event-driven): Upload ảnh (S3) $\rightarrow$ Trigger $\rightarrow$ Resize $\rightarrow$ Storage. <br>- **Thực hành:** <br>  + Xử lý ảnh: Viết Lambda Function (Node.js), cấu hình biến môi trường và thiết lập S3 Trigger (All object create events). <br>  + Quản lý dữ liệu: Tạo bảng DynamoDB (On-demand) và viết Lambda (Python) để lưu trữ metadata sách. <br>  + Bảo mật: Cấu hình IAM Policy tuân thủ nguyên tắc Least Privilege (Quyền tối thiểu). | 20/10/2025   | 20/10/2025      | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3   | CHỦ ĐỀ: XÂY DỰNG ỨNG DỤNG SERVERLESS (FULL STACK) <br>- Lý thuyết nền tảng: <br>  + Amazon API Gateway: Vai trò "cửa ngõ" quản lý traffic, xác thực và các loại API (RESTful). <br>  + S3 Static Web Hosting: Cơ chế lưu trữ và phân phối Frontend web không cần máy chủ. <br>- **Thực hành:** <br>  + Frontend Deployment: Build source code ReactJS, upload lên S3 bucket và cấu hình quyền truy cập public. <br>  + Backend Development: Phát triển chuỗi Lambda function xử lý nghiệp vụ CRUD (Create, Read, Delete). <br>  + Tích hợp hệ thống: Thiết lập API Gateway, xử lý vấn đề CORS và kết nối Frontend với Backend thông qua API Endpoint.             | 21/10/2025 | 21/10/2025      | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4   | CHỦ ĐỀ: HỆ THỐNG XỬ LÝ ĐƠN HÀNG (DECOUPLING ARCHITECTURE) <br>- Kiến trúc hệ thống: <br>  + Mô hình Bất đồng bộ (Asynchronous): Tách rời (decouple) các thành phần hệ thống để tăng khả năng mở rộng. <br>  + Messaging Services: Sử dụng Amazon SQS làm bộ đệm chịu tải và Amazon SNS để gửi thông báo. <br>- **Thực hành:** <br>  + Infrastructure as Code: Sử dụng AWS SAM để định nghĩa và deploy toàn bộ stack (API, Lambda, DB, Queue). <br>  + Xử lý logic: Cấu hình Lambda đẩy message vào Queue và Worker xử lý đơn hàng từ Queue vào DynamoDB. <br>  + Kiểm thử & Verify: Thực hiện luồng End-to-End từ đặt hàng, kiểm tra SQS flight-mode đến nhận email SNS. | 22/10/2025   | 22/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5   | CHỦ ĐỀ: ÔN TẬP THIẾT KẾ KIẾN TRÚC BẢO MẬT (SECURE ARCHITECTURES) <br>- Nội dung nghiên cứu: <br>  + Quản lý truy cập: Đào sâu về IAM Roles, Policies, MFA và Service Control Policies (SCP). <br>  + Bảo vệ hạ tầng: Phân biệt Security Groups (Stateful) và NACLs (Stateless). <br>  + Các dịch vụ bảo mật nâng cao: AWS WAF, AWS Shield, GuardDuty và Secrets Manager. <br>- **Thực hành:** <br>  + Rà soát bảo mật: Kiểm tra lại các Security Group và IAM Role đã thiết lập trong các bài Lab tuần này. <br>  + Encryption: Tìm hiểu cơ chế mã hóa dữ liệu nghỉ (KMS) và dữ liệu đường truyền (TLS/ACM).               | 23/10/2025   | 23/10/2025      | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6   | CHỦ ĐỀ: ÔN TẬP THIẾT KẾ KIẾN TRÚC BỀN VỮNG (RESILIENT ARCHITECTURES) <br>- Nội dung nghiên cứu: <br>  + Tính sẵn sàng cao (High Availability): Thiết kế Multi-AZ và Multi-Region. <br>  + Phục hồi thảm họa (Disaster Recovery): Các chiến lược từ Backup & Restore đến Multi-site Active/Active. <br>  + Khả năng mở rộng: Ôn tập về EC2 Auto Scaling, DynamoDB Scaling và Route 53 Routing Policies. <br>- **Thực hành:** <br>  + Dọn dẹp tài nguyên (Cleanup): Xóa Stack SAM, Empty S3 Buckets và xóa DynamoDB Tables để tránh phát sinh chi phí.                 | 24/10/2025 | 24/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |


### Kết quả đạt được tuần 7:
* **Vận hành thành thạo mô hình Event-Driven (Hướng sự kiện)**
  * Xây dựng thành công luồng xử lý tự động: S3 Event Trigger kích hoạt Lambda Function để xử lý hình ảnh và lưu metadata, loại bỏ hoàn toàn can thiệp thủ công.
* **Triển khai ứng dụng Full-stack Serverless toàn diện**
  * Hoàn thiện ứng dụng Book Store với Frontend (S3 Static Hosting) giao tiếp bảo mật với Backend qua Amazon API Gateway.
  * Thiết kế cơ sở dữ liệu DynamoDB chế độ On-demand phù hợp với workload không ổn định.
* **Hiện thực hóa kiến trúc Decoupling (Tách rời hệ thống)**
  * Ứng dụng thành công Amazon SQS (Queue) và Amazon SNS (Topic) để xử lý đơn hàng bất đồng bộ, giúp hệ thống chịu tải cao và đảm bảo trải nghiệm người dùng không bị gián đoạn.
* **Làm chủ Infrastructure as Code (IaC) với AWS SAM**
  * Thay vì thao tác thủ công dễ sai sót, đã biết cách định nghĩa, build và deploy toàn bộ stack phức tạp (API, DB, Lambda, Queue) thông qua mã nguồn `template.yaml`.

### Khó khăn – Giải pháp:
* **Lỗi kết nối Cross-Origin (CORS) giữa Frontend và Backend**
  * Frontend trên S3 bị trình duyệt chặn khi gọi API Gateway.
  * **Giải pháp:** Cấu hình Enable CORS trên API Gateway cho tất cả các methods (GET, POST, DELETE). Quan trọng nhất là phải **Deploy API** lại ngay sau khi sửa đổi cấu hình thì thay đổi mới có hiệu lực.
* **Lambda Function báo lỗi "Access Denied" khi truy xuất tài nguyên**
  * Function không thể ghi file vào S3 bucket đích hoặc không thể Scan bảng DynamoDB.
  * **Giải pháp:** Kiểm tra CloudWatch Logs để xác định quyền bị thiếu. Cập nhật IAM Role của Lambda theo nguyên tắc cấp quyền cụ thể (Inline Policy) thay vì dùng quyền FullAccess quá rộng.
* **Xử lý trùng lặp tin nhắn trong Amazon SQS**
  * Đơn hàng đã được lưu vào Database nhưng tin nhắn vẫn tồn tại trong Queue (Flight mode) dẫn đến nguy cơ xử lý lại.
  * **Giải pháp:** Rà soát logic code trong Lambda Worker (`handle_order`), đảm bảo lệnh `sqs.delete_message` được thực thi ngay sau khi tác vụ ghi Database thành công (trong khối `try...except`).

### Bài học rút ra:
* **Sức mạnh của kiến trúc Bất đồng bộ (Asynchronous)**
  * Việc đặt SQS vào giữa Frontend và Backend là chìa khóa cho các hệ thống quy mô lớn, giúp "giảm xóc" (buffer) khi lượng truy cập tăng đột biến mà không làm sập Database.
* **Nguyên tắc Least Privilege (Quyền tối thiểu) là sống còn**
  * Trong môi trường Lab có thể dùng quyền rộng, nhưng thực tế (Production) phải giới hạn quyền trên từng Resource ARN cụ thể để đảm bảo an ninh hệ thống.
* **Tư duy "Design for Failure" (Thiết kế cho sự cố)**
  * Hệ thống không được thiết kế để "không bao giờ hỏng", mà phải có khả năng tự phục hồi. Việc sử dụng Auto Scaling, Multi-AZ và Route 53 Failover là bắt buộc để đảm bảo tính bền vững (Resilience).