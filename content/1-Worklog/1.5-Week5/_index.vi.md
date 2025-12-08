---
title: "Worklog Tuần 5"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :---: | :---: | :--- |
| 2 | CHỦ ĐỀ: QUẢN TRỊ SERVER KHÔNG CẦN BASTION HOST (SSM PART 1) <br> - **Lý thuyết:** <br>  + **Session Manager:** Tìm hiểu cơ chế quản trị server thay thế SSH/RDP truyền thống, loại bỏ hoàn toàn Bastion Host. <br>  + **Kiến trúc bảo mật:** Phân tích mô hình IAM Role kết hợp SSM Agent và giao thức TLS 1.2. <br>  + **Lợi ích:** Giảm thiểu bề mặt tấn công do không cần mở port 22 (Linux) hay 3389 (Windows) ra Internet. <br> - **Thực hành:** <br>  + **Thiết lập mạng:** Tạo VPC & Subnets (Public/Private) chuẩn bị cho môi trường lab. <br>  + **Security Group (Zero Trust):** Cấu hình SG đóng toàn bộ Inbound traffic, chỉ cho phép Outbound HTTPS. <br>  + **Kết nối cơ bản:** Khởi tạo EC2 (Linux & Windows), gán IAM Role `AmazonSSMManagedInstanceCore` và thực hiện kết nối trực tiếp qua trình duyệt (Browser-based). | 06/10/2025 | 06/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | CHỦ ĐỀ: KẾT NỐI RIÊNG TƯ & AUDIT LOGGING (SSM PART 2) <br> - **Lý thuyết:** <br>  + **VPC Endpoints (PrivateLink):** Hiểu cơ chế giúp Private Instance giao tiếp với AWS Services qua mạng nội bộ mà không cần Internet Gateway. <br>  + **Port Forwarding:** Kỹ thuật đường hầm (tunneling) để truy cập RDP/SSH an toàn. <br> - **Thực hành:** <br>  + **Cấu hình Endpoints:** Triển khai 3 Interface Endpoints (`ssm`, `ssmmessages`, `ec2messages`) cho Private Subnet. <br>  + **Quản lý Logs:** Tạo S3 Gateway Endpoint và cấu hình Session Manager để đẩy toàn bộ lịch sử lệnh (command history) về S3 bucket (có mã hóa). <br>  + **Kết nối nâng cao:** Cài đặt AWS CLI và Plugin trên máy cá nhân, thực hiện Port Forwarding để RDP vào Private Windows Instance (Port 3389 -\> Localhost 9999). | 07/10/2025 | 07/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | CHỦ ĐỀ: HẠ TẦNG DƯỚI DẠNG MÃ (INFRASTRUCTURE AS CODE - CLOUDFORMATION) <br> - **Lý thuyết:** <br>  + **Cấu trúc Template:** Nắm vững các thành phần Parameters, Resources, Outputs và các hàm nội tại (`!Ref`, `!Sub`, `!GetAtt`). <br>  + **Khái niệm Drift:** Hiểu về sự sai lệch giữa cấu hình thực tế và cấu hình trong code. <br> - **Thực hành:** <br>  + **Môi trường:** Thiết lập IDE AWS Cloud9 để viết code. <br>  + **Viết Template:** Xây dựng file YAML tự động hóa việc tạo Security Group, IAM Role và EC2 Instance. <br>  + **Custom Resources:** Sử dụng Lambda Function để tạo SSH Key Pair và lưu vào Parameter Store (xử lý tác vụ CFN không hỗ trợ sẵn). <br>  + **StackSets & Drift:** Triển khai hạ tầng đồng loạt trên nhiều Region và thực hành kỹ thuật phát hiện sai lệch cấu hình (Detect Drift). | 08/10/2025 | 08/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | CHỦ ĐỀ: BẢO VỆ ỨNG DỤNG WEB VỚI AWS WAF <br> - **Lý thuyết:** <br>  + **Web ACL & Rules:** Phân biệt AWS Managed Rules (có sẵn) và Custom Rules (tự định nghĩa). <br>  + **Logic xử lý:** Hiểu các hành động Block, Allow, Count và cấu trúc JSON cho các rule phức tạp. <br> - **Thực hành:** <br>  + **Triển khai:** Deploy ứng dụng mẫu OWASP Juice Shop qua CloudFormation và tạo Web ACL bảo vệ. <br>  + **Áp dụng Rules:** Kích hoạt Managed Rules (Core Rule Set, SQL Database) để chặn SQL Injection và XSS. <br>  + **Custom Rules:** Viết rule tùy chỉnh bằng JSON (kết hợp logic AND/OR) để chặn các Header hoặc Query String cụ thể. <br>  + **Logging:** Thiết lập Kinesis Data Firehose để đẩy log WAF về S3, cấu hình Redacted Fields để ẩn thông tin nhạy cảm (Cookie/Auth Token). | 09/10/2025 | 09/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | CHỦ ĐỀ: MÃ HÓA & QUẢN TRỊ KHÓA (KMS & CLOUDTRAIL) <br> - **Lý thuyết:** <br>  + **Key Management:** Phân biệt Symmetric (đối xứng) và Asymmetric Key (bất đối xứng). <br>  + **SSE-KMS:** Cơ chế mã hóa phía máy chủ (Server-side Encryption) tích hợp với S3. <br> - **Thực hành:** <br>  + **Quản trị Key:** Tạo Customer Managed Key (CMK), thiết lập Alias và bật tính năng tự động xoay vòng khóa (Key Rotation). <br>  + **Bảo mật S3:** Tạo Bucket bắt buộc mã hóa bằng KMS Key, kiểm thử quyền truy cập (User không có quyền Key sẽ bị chặn dù có quyền S3). <br>  + **Audit & Share:** Sử dụng CloudTrail và Athena để truy vấn nhật ký truy cập. Thực hành chia sẻ file an toàn bằng Presigned URL có thời hạn. <br>  + **Dọn dẹp:** Thực hiện quy trình xóa tài nguyên an toàn (Schedule Key Deletion, Delete Stack/Buckets) để tối ưu chi phí. | 10/10/2025 | 10/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Kết quả đạt được tuần 5:
* **Quản trị máy chủ chuẩn Zero Trust:** Loại bỏ hoàn toàn sự phụ thuộc vào Bastion Host và việc mở port 22/3389. Vận hành thành công Session Manager kết hợp VPC Endpoints để quản lý Private Instance mà không cần Internet Gateway.
* **Tự động hóa hạ tầng (IaC):** Chuyển đổi tư duy từ thao tác thủ công sang Infrastructure as Code với CloudFormation. Đã xử lý được các bài toán nâng cao như Custom Resources (dùng Lambda tạo Key) và kiểm soát sai lệch tài nguyên (Drift Detection).
* **Bảo mật đa lớp (Defense in Depth):** Triển khai tường lửa ứng dụng WAF (Layer 7) ngăn chặn lỗ hổng OWASP và thiết lập mã hóa dữ liệu 2 lớp với KMS (Data Layer), đảm bảo an toàn từ đường truyền đến lưu trữ.

### Khó khăn – Giải pháp:
* SSM Agent trên Private Instance không hoạt động (Offline)
  * Giải pháp: Rà soát lại hạ tầng mạng. Đã bổ sung đủ 3 endpoints bắt buộc (`ssm`, `ssmmessages`, `ec2messages`) vào Private Subnet và đảm bảo Security Group của Endpoint cho phép Port 443 từ dải mạng VPC.
  
* File S3 đã cấu hình "Make Public" nhưng truy cập vẫn báo lỗi Access Denied/Signature
  * Giải pháp: Nguyên nhân do file được mã hóa bằng KMS Key và người dùng ẩn danh (Anonymous) không có quyền giải mã. Chuyển sang sử dụng **Presigned URL** để chia sẻ file an toàn có thời hạn thay vì mở Public ACL.

* WAF Rule chặn nhầm người dùng hợp lệ (False Positive) khi mới triển khai
  * Giải pháp: Thay đổi quy trình deployment. Luôn thiết lập Action là **"Count"** để theo dõi Metrics trên CloudWatch trước, sau khi xác nhận không ảnh hưởng user thật mới chuyển sang **"Block"**.

### Bài học rút ra:
* Trong môi trường Cloud, bảo mật không chỉ là chặn IP. Việc quản lý định danh (IAM Role) cấp quyền cho máy chủ và dịch vụ (Service-to-Service) mới là cốt lõi, thay thế cho tư duy mở port truyền thống.
* Áp dụng bảo mật chiều sâu: Network (VPC/SG) -> Application (WAF) -> Data (KMS). Ngay cả khi file S3 bị lộ đường dẫn (Public), kẻ tấn công vẫn không thể đọc nội dung nếu không có Key giải mã.
