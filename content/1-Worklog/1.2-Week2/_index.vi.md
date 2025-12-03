---
title: "Worklog Tuần 2"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Thực hành triển khai hạ tầng mạng và compute cơ bản.
* Triển khai Amazon VPC với kiến trúc đầy đủ (Public & Private Subnet, gắn Internet Gateway, cấu hình Route Tables, Security Groups, NAT Gateway).
* Triển khai Amazon EC2 Instances (Linux & Windows), kết nối bằng SSH và RDP.
* Thực hành nguyên tắc bảo mật least privilege trong Security Groups.
* Thực hành triển khai ứng dụng Node.js User Management trên Amazon Windows Server 2022.
* Rèn luyện kỹ năng quản lý chi phí AWS, dọn dẹp tài nguyên sau mỗi lab.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2   | - Ôn lại lý thuyết Amazon VPC <br> - Tìm hiểu lý thuyết về Amazon EC2 Instances <br> - **Thực hành:** <br>&emsp; + Tạo VPC với CIDR 10.10.0.0/16 và cấu hình DNS <br>&emsp; + Tạo Subnet và bật Auto-assign IP cho Public Subnet <br>&emsp; + Tạo Internet Gateway và gắn vào VPC. <br>&emsp; + Tạo Route Table Public, cấu hình route 0.0.0.0/0 → IGW <br>&emsp; +Tạo Security Group cho Public Subnet (SSH, ICMP). <br>&emsp; + Tạo Security Group cho Private Subnet (SSH từ Public SG). <br>&emsp; + Tạo Security Group cho VPC Endpoint (HTTPS nội bộ).   | 15/09/2025   | 15/09/2025      |
| 3   | - Triển khai Amazon EC2 Instances <br>&emsp; + Tạo EC2 Instance trong Public Subnet và Private Subnet <br>&emsp; + Kết nối SSH: local → EC2 Public → EC2 Private (qua IP private)  <br>&emsp; + Thao tác với key pair (aws-keypair.pem/.ppk) qua PuTTY, pscp, chmod 400 để kết nối tới máy chủ EC2. <br>&emsp; + Kiểm tra ping Internet từ Public EC2 và Private EC2 instances. <br>&emsp; + Tạo Elastic IP và NAT Gateway trong public subnet cho phép các instances trong private subnet kết nối ra internet.      | 16/09/2025   | 16/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Khởi tạo EC2 Windows Server 2022. <br>&emsp; + Kết nối đến Windows instance trên AWS EC2 qua RDP. <br> &emsp; + Khởi tạo Amazon Linux 2 instance <br> &emsp; + Kết nối đến EC2 Linux instance sử dụng MobaXterm và PuTTY. | 17/09/2025   | 17/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu Amazon EC2 cơ bản và thực hành những tác vụ cơ bản như thay đổi cấu hình, tạo snapshot, xây dựng AMI tùy chọn, truy cập khi mất key pair.     | 18/09/2025   | 18/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Tìm hiểu lý thuyết triển khai ứng dụng ứng dụng AWS User Management Node.js trên Amazon Linux. <br> - **Thực hành:** <br>&emsp; + Cài đặt XAMPP (Apache + MySQL) trên Windows Server 2022. <br>&emsp; + Tạo database và table user qua giao diện phpMyAdmin. <br>&emsp; + Cài đặt Node.js + Git trên Windows instance. <br>&emsp; + Clone repo code, npm init, cài các dependencies. <br>&emsp; + Tạo file .env cấu hình DB, dùng Nodemon và npm start để chạy app và tiết kiệm thời gian.                     | 19/09/2025   | 19/09/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Hoàn thiện kiến trúc mạng VPC với Subnet, IGW, Route Tables.

* Tạo đầy đủ SG cho Public, Private, VPC Endpoint.

* Private EC2 ping Internet thành công (qua NAT Gateway).

* EC2 Linux: Triển khai EC2 Public & Private, SSH kết nối thành công.

* EC2 Windows: Khởi tạo, kết nối RDP thành công.

* Cài XAMPP, Node.js, deploy CRUD app User Management thành công.
  
* Quản lý chi phí AWS, dọn dẹp tài nguyên sau mỗi lab.

### Khó khăn – Giải pháp:
* EC2 Private không ping được Internet.
  * Giải pháp: Tạo NAT Gateway + Route Table Private.

* Lỗi kết nối SSH tới EC2 Private
  * Giải pháp: Kiểm tra Security Group, Route Table, NAT Gateway, SSH qua EC2 Public (bastion host).

* RDP Windows bị lỗi password/decrypt.
  * Giải pháp: Mỗi lần stop/ start instance, IP đổi, tải lại file remote desktop mới. Giải mã password bằng key pair .pem, xem lại rule cổng 3389 trong SG.
  
### Bài học rút ra:
* Tuân thủ nguyên tắc bảo mật least privilege trong cấu hình Security Groups.
* Hiểu Public vs Private Subnet, cơ chế NAT Gateway.
* Nắm các thao tác cơ bản với EC2: thay đổi cấu hình, tạo snapshot, xây dựng AMI tùy chọn, truy cập khi mất key pair.
* Biết cách RDP quản trị Windows Server trên AWS EC2. SSH quản trị Linux Server trên AWS EC2.

### Kế hoạch tuần tiếp theo: