---
title: "Worklog Tuần 3"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Nắm vững cách cấu hình IAM Role cho EC2, hiểu rõ cơ chế Security Token Service (STS) cấp quyền tạm thời thay vì nhúng Access Key.
* Triển khai hoàn chỉnh S3 Static Website được bảo mật (BPA) và tăng tốc qua CloudFront (sử dụng OAI).
* Thực hành các tính năng quản trị S3 quan trọng, bao gồm S3 Versioning và Cross-Region Replication (CRR).
* Xây dựng hạ tầng mạng 3-tier (Web - App - DB) trên AWS với VPC, SSecurity Group (phân tách EC2/RDS) và DB Subnet Group (đa AZ).
* Triển khai ứng dụng Node.js kết nối Amazon RDS (MySQL).
* Hiểu thao tác restore (Snapshot) và phân biệt rõ Multi-AZ với Read Replicas.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | - **Tìm hiểu lý thuyết:**<br>  + Hai phương thức cấp quyền: Access Key (nhúng key, rủi ro cao) và IAM Role (thông tin tạm thời, bảo mật, khuyến khích sử dụng).<br>  + Hiểu cơ chế hoạt động của IAM Role trên EC2 (EC2 Instance Profile) và vai trò của Security Token Service (STS).<br>- **Thực hành:**<br> + Setup môi trường (EC2 t2.micro, S3 Bucket).<br>  + *Access Key:* Tạo IAM User, cấp quyền Programmatic access, nhúng Access Key vào code Python (boto3) để upload file lên S3 <br>  + *Bảo mật (IAM Role):* Cấu hình thành công IAM Role (Instance Profile) cho EC2, AWS CLI tự động nhận diện quyền qua metadata mà không cần file credentials.<br>  + Dọn dẹp tài nguyên (EC2, S3, IAM User/Role). | 22/09/2025 | 22/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | - **Tìm hiểu lý thuyết:**<br>  + Tổng quan về AWS Cloud9: Là một IDE tích hợp hoạt động trên trình duyệt, cung cấp trình sửa mã, debugger và terminal tích hợp.<br>  + AWS CLI đã được cài đặt và cấu hình sẵn trên Cloud9.<br>- **Thực hành:** <br>  + Setup môi trường Cloud9 (t2.micro). **Note:** Cloud9 tự động quản lý EC2 backend và cài sẵn AWS CLI.<br>  + Thao tác cơ bản giao diện terminal tích hợp và trình chỉnh sửa code (mở, sửa, lưu file).<br>  + Kiểm tra thành công AWS CLI `aws ec2 describe-instances`.<br>  + Dọn dẹp: Xóa Cloud9 environment. | 23/09/2025 | 23/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | - **Tìm hiểu lý thuyết:**<br>  + Amazon S3: Dịch vụ lưu trữ đối tượng (độ bền 11 số 9). Phân biệt Bucket (tên duy nhất toàn cầu) và Object.<br>  + Tính năng S3: Static Website Hosting, S3 Versioning (chống xóa/ghi đè, tạo "delete marker"), Cross-Region Replication (CRR) (khôi phục thảm họa, yêu cầu bật Versioning).<br>  + Bảo mật & Hiệu suất: Block Public Access (BPA) (nên luôn bật). Sử dụng CloudFront với OAC (Origin Access Control) để bảo mật và tăng tốc (phân phối qua Edge Location). | 24/09/2025 | 24/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | - **Thực hành:**<br> + *Giai đoạn 1 (Public S3):* Triển khai S3 Static Website. Tạm thời tắt Block Public Access (BPA) và cấu hình ACLs (Make public using ACL) để public website (ghi nhận đây là cách không khuyến nghị).<br>  + *Giai đoạn 2 (Private S3 + CloudFront):* Tái cấu hình bảo mật: Bật BPA (=> private bucket). Tích hợp CloudFront với OAI (Origin Access Identity), cho phép CloudFront truy cập S3 trong khi khóa truy cập public.<br>  + **Kết quả:** Tốc độ tải trang cải thiện rõ rệt khi truy cập qua CloudFront URL.<br>  + *Giai đoạn 3 (Tính năng):* Kích hoạt S3 Versioning để kiểm tra khả năng khôi phục. Cấu hình Cross-Region Replication (CRR) sang region khác.<br>  + Dọn dẹp tài nguyên (CloudFront, S3 Buckets). | 25/09/2025 | 25/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | - **Tìm hiểu lý thuyết:**<br>  + Amazon RDS: Dịch vụ DB quan hệ được quản lý (cho OLTP), tự động vá lỗi, backup.<br>  + HA/DR: Phân biệt Multi-AZ (HA, sao chép đồng bộ, failover tự động) và Read Replicas (Mở rộng đọc, sao chép không đồng bộ).<br>  + Mạng: Vai trò của DB Subnet Group (cần ít nhất 2 AZ cho Multi-AZ) và Security Group (mở cổng 3306 chỉ từ EC2 SG).<br>- **Thực hành:**<br>  + **Bài học:** Xây dựng hạ tầng mạng và triển khai ứng dụng 3-tier (Web - App - DB).<br>  + *Chuẩn bị mạng (Nền tảng):* Hoàn thành setup hạ tầng VPC. **Ghi nhận mấu chốt:** Cấu hình 2 Security Group riêng biệt (EC2, RDS) và DB Subnet Group (sử dụng 2 AZ) là điều kiện tiên quyết để RDS hoạt động bảo mật và hỗ trợ Multi-AZ.<br>  + *Triển khai:* Khởi tạo EC2 (Web server) và RDS (MySQL). Cài đặt ứng dụng Node.js trên EC2 và kết nối thành công tới RDS endpoint.<br>  + *Vận hành DB:* Thực thi script SQL để tạo schema. **Thử nghiệm restore snapshot, ghi nhận:** RDS tạo ra một instance *mới* với endpoint *mới* (đòi hỏi phải cập nhật config ứng dụng).<br>  + Dọn dẹp toàn bộ tài nguyên (RDS, EC2, VPC). | 26/09/2025 | 26/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Kết quả đạt được tuần 3:
* Phân biệt rõ ràng và vận dụng đúng phương thức cấp quyền truy cập 
* Triển khai thành công Static Website bảo mật và hiệu suất cao
* Nắm quy trình triển khai hạ tầng mạng và ứng dụng 3-tier: Hiểu được tính logic và tuần tự khi setup hạ tầng mạng. Đã cấu hình thành công các thành phần cốt lõi: VPC , Security Group (chia tách SG cho EC2 và RDS) , và DB Subnet Group (chuẩn bị cho Multi-AZ)
* Vận hành cơ bản Amazon RDS. Khi khôi phục từ DB Snapshot, RDS sẽ tạo ra một DB instance mới với một endpoint mới, đòi hỏi phải cập nhật chuỗi kết nối trong ứng dụng.

### Khó khăn – Giải pháp:
* Cấu hình Cross-Region Replication (CRR) nhưng file mới upload ở bucket nguồn không tự động sao chép sang bucket đích
  * Giải pháp: Kiểm tra lại IAM Role của S3. Cần cấp quyền s3:GetReplicationConfiguration và s3:ListBucket cho bucket nguồn, và s3:ReplicateObject cho bucket đích.
  
* Ứng dụng trên EC2 không thể kết nối tới RDS Database (lỗi timeout)
  * Giải pháp: Kiểm tra RDS Security Group. Mở cổng 3306 (MySQL) nhưng Source là IP public của EC2 nên thay đổi Source thành Security Group ID của EC2 đảm bảo kết nối nội bộ an toàn trong VPC.
  

### Bài học rút ra:
* Bảo mật là ưu tiên
  * Không nhúng cứng credentials (Access Key). Sử dụng IAM Role cho các tài nguyên AWS (như EC2) để cấp quyền tạm thời.
  * Luôn bật Block Public Access (BPA) cho S3. Chỉ cho phép truy cập S3 thông qua các dịch vụ tin cậy (như CloudFront OAI/OAC).
  * Không mở cổng quản trị (SSH) hoặc cổng DB (3306) ra 0.0.0.0/0. Phải giới hạn IP nguồn (cho SSH) hoặc giới hạn bằng Security Group (cho DB).
* Endpoint: Khi làm việc với các dịch vụ (S3 Static Website, CloudFront, RDS), endpoint (URL) là chìa khóa truy cập. Bất kỳ thay đổi nào về endpoint (như restore RDS hoặc chuyển sang CloudFront ) đều phải được cập nhật ở phía ứng dụng.
* Các tính năng được quản lý như S3 Versioning (bảo vệ dữ liệu) , Multi-AZ (tăng HA) , và Cloud9 cost-saving (tiết kiệm chi phí) giúp tối ưu hóa vận hành.
