---
title: "Worklog Tuần 1"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:

* Giao lưu, kết nối với các thành viên và làm quen với môi trường học tập tại First Cloud Journey.
* Hiểu và nắm được các dịch vụ cơ bản của AWS.
* Thực hành các bước khởi tạo và cấu hình tài khoản AWS Free Tier.
* Bắt đầu làm quen với AWS Management Console và AWS CLI.
* Tìm hiểu về Amazon VPC và các thành phần mạng cơ bản.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc       | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Làm quen với các thành viên FCJ. <br> - Đọc và lưu ý các nội quy, quy định tại đơn vị thực tập.                                                                                             | 08/09/2025   | 08/09/2025      |
| 3   | - Tạo AWS Free Tier account. <br> - Tìm hiểu AWS và tổng quan về các nhóm dịch vụ <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + Monitoring <br>&emsp; + Quản lý chi phí <br>                                            | 09/09/2025   | 09/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Thiết lập MFA cho root user và admin user. <br> - Làm quen AWS Management Console (EC2, S3, RDS, Lambda, CloudWatch). <br> - Tìm hiểu về AWS Budget. <br> - **Thực hành:** <br>&emsp; + Thiết lập MFA (Multi-factor Authentication). <br>&emsp; + Tạo Admin Group và Admin User thay cho root để quản lý tài nguyên AWS. <br>&emsp; + Tạo Cost Budget, Usage Budget, RI Budget, Savings Plans Budget. | 10/09/2025   | 10/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Nghiên cứu AWS Support và các gói dịch vụ hỗ trợ: <br>&emsp; + Gói Basic <br>&emsp; + Gói Developer <br>&emsp; + Gói Business <br>&emsp; + Gói Enterprise <br> - Học quản trị quyền truy cập với IAM. <br> - **Thực hành:** <br>&emsp; + Tạo và quản lý IAM Groups, IAM Users. <br>&emsp; + Triển khai IAM Roles với quyền tạm thời. <br> - Tìm hiểu Elastic IP   <br>                  | 11/09/2025   | 11/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tìm hiểu tổng quan về Amazon VPC. <br> - Nắm các khái niệm: CIDR, Subnet, Route Table, Internet Gateway, NAT Gateway. <br> - Tìm hiểu tổng quan tường lửa trong Amazon VPC                   | 12/09/2025   | 12/09/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 1:

* Hiểu AWS là gì và nắm được các nhóm dịch vụ cơ bản: 
  * Compute
  * Storage
  * Networking 
  * Database

* Thiết lập thành công AWS Free Tier account an toàn với MFA và IAM chuẩn.

* Làm quen với AWS Management Console và biết cách tìm, truy cập, sử dụng dịch vụ từ giao diện web. 

* Biết cách liên hệ và tạo case trên AWS Support.

* Hiểu lý thuyết kiến trúc mạng AWS VPC và vai trò các thành phần cơ bản.

### Khó khăn – Giải pháp:
* Khó khăn ban đầu trong việc phân biệt root user và IAM user.
  * Giải pháp: thực hành tạo Admin Group và Admin User thay cho root để quản lý tài nguyên AWS.
* Một số khái niệm như CIDR, Subnet, Internet Gateway, NAT Gateway, RI, Savings Plans còn mới mẻ.
  * Giải pháp: tham khảo tài liệu, ghi chú lại để dễ ghi nhớ và hiểu sâu hơn.
  
### Bài học rút ra:
* Không sử dụng root user cho tác vụ bình thường để đảm bảo an toàn cho tài khoản AWS, luôn bật MFA cho root user và các IAM user quan trọng.
* Chủ động quản lý chi phí, đặt ngưỡng cảnh báo rõ ràng.

### Kế hoạch tuần tiếp theo:
* Thực hành triển khai Amazon VPC.
* Thực hành triển khai EC2 instance và kết nối với S3.
* Tiếp tục mở rộng kiến thức networking với VPC Peering và Security Groups.