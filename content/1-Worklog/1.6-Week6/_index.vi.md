---
title: "Worklog Tuần 6"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
* **Làm chủ quản lý định danh và phân quyền (Identity & Access Management):**
    * Chuyển đổi tư duy từ quản lý User cục bộ sang quản lý tập trung với **IAM Identity Center**.
    * Nắm vững kiến trúc bảo mật đa lớp thông qua **Permission Boundary** (chặn leo thang quyền) và **IAM Role Conditions** (kiểm soát ngữ cảnh truy cập).
* **Quản trị tư thế bảo mật (Security Governance):** Hiểu và vận hành **AWS Security Hub** để tự động đánh giá mức độ tuân thủ của hệ thống theo các tiêu chuẩn quốc tế (CIS, PCI DSS).
* **Đảm bảo an toàn và khả năng khôi phục dữ liệu:** Xây dựng chiến lược sao lưu tự động với **AWS Backup**, tập trung vào tư duy "Recovery Testing" (kiểm thử khôi phục) tự động hóa.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | CHỦ ĐỀ: QUẢN LÝ ĐỊNH DANH TẬP TRUNG VỚI IAM IDENTITY CENTER <br> - Kiến trúc & Cơ chế hoạt động: <br>  + Hiểu mô hình xác thực tập trung (SSO) cho môi trường Multi-account và vai trò của Permission Sets. <br>  + Phân tích các mô hình kiểm soát quyền nâng cao: Customer Managed Policies và Time-based Access Control. <br> - **Thực hành:** <br>  + Setup hạ tầng: Khởi tạo AWS Organizations và kích hoạt IAM Identity Center. <br>  + Quản trị User/Group: Tạo nhóm `Administrators` & `readOnly`, thiết lập user và chính sách mật khẩu. <br>  + Phân quyền & Provisioning: Tạo Permission Sets (`AdministratorAccess`, `ViewOnlyAccess`) và gán quyền tự động xuống tài khoản đích. <br>  + Tích hợp CLI: Cấu hình `aws configure sso` để xác thực chuẩn OIDC qua dòng lệnh. | 13/10/2025 | 13/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | CHỦ ĐỀ: KIỂM SOÁT QUYỀN HẠN VỚI PERMISSION BOUNDARY <br> - Lý thuyết & Tư duy bảo mật: <br>  + Định nghĩa "Permission Boundary" và cơ chế "Effective Permissions" (Giao thoa giữa quyền được cấp và giới hạn). <br>  + Phân tích Use-case ngăn chặn leo thang đặc quyền (Privilege Escalation) trong doanh nghiệp. <br> - **Thực hành:** <br>  + Tạo Boundary Policy: Viết chính sách JSON giới hạn thao tác EC2 chỉ trong Region Singapore (`ap-southeast-1`). <br>  + Cấu hình User: Tạo User `ec2-admin` được cấp Full Access nhưng bị gán Permission Boundary. <br>  + Kiểm thử (Verification): Xác thực việc User bị chặn khi thao tác tại Region khác (Sydney) dù có quyền Admin. | 14/10/2025 | 14/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | CHỦ ĐỀ: CƠ CHẾ IAM ROLE & ĐIỀU KIỆN TRUY CẬP (CONDITIONS) <br> - Các khái niệm cốt lõi: <br>  + Phân biệt Principal, Identities (User/Group/Role) và cơ chế xác thực. <br>  + Nắm vững quy trình Assume Role và vai trò của AWS STS (Security Token Service). <br> - **Thực hành:** <br>  + Quản lý User/Group: Tạo nhóm quản trị `ec2-rds-admin` và các user chức năng. <br>  + Cấu hình Switch Role: Tạo IAM Role, thiết lập Trust Relationship cho phép User thường (`No-permission-user`) thực hiện Assume Role. <br>  + Bảo mật nâng cao: Thêm Conditions vào Trust Policy để giới hạn quyền Switch Role theo địa chỉ IP nguồn và khung thời gian cụ thể. | 15/10/2025 | 15/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | CHỦ ĐỀ: QUẢN TRỊ BẢO MẬT TỰ ĐỘNG VỚI SECURITY HUB <br> - Tiêu chuẩn & Đánh giá: <br>  + Tìm hiểu các bộ tiêu chuẩn: CIS AWS Foundations, PCI DSS và AWS Foundational Security Best Practices. <br>  + Hiểu cơ chế chấm điểm (Security Score) và mối liên hệ với AWS Config. <br> - **Thực hành:** <br>  + Kích hoạt & Cấu hình: Enable Security Hub, bật các bộ tiêu chuẩn và cấu hình AWS Config (Recording). <br>  + Giám sát & Tinh chỉnh: Phân tích các Findings, thực hiện vô hiệu hóa (Suppress) các quy tắc không phù hợp với môi trường Lab. <br>  + Resource Cleanup: Vô hiệu hóa dịch vụ đúng cách để tối ưu chi phí. | 16/10/2025 | 16/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | CHỦ ĐỀ: CHIẾN LƯỢC SAO LƯU & KHÔI PHỤC TỰ ĐỘNG (AWS BACKUP) <br> - Lý thuyết Backup & Restore: <br>  + Định nghĩa chỉ số RTO (Recovery Time Objective) và RPO (Recovery Point Objective). <br>  + Kiến trúc AWS Backup: Backup Plan, Vault và cơ chế thông báo (Notifications). <br> - **Thực hành:** <br>  + Infrastructure as Code: Dùng CloudFormation triển khai hạ tầng giả lập (EC2, Lambda, SNS). <br>  + Cấu hình Backup: Tạo Vault, thiết lập Backup Plan tự động và gán tài nguyên qua Tags. <br>  + Automation Workflow: Thực hiện On-demand Backup, kích hoạt Lambda tự động Restore và kiểm tra tính toàn vẹn dữ liệu ngay khi Backup hoàn tất. | 17/10/2025 | 17/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |


### Kết quả đạt được tuần 6:
* Chuyển đổi tư duy quản trị từ IAM User đơn lẻ sang mô hình định danh tập trung (Identity Center), giải quyết bài toán quản lý truy cập quy mô lớn (Multi-account).
* Triển khai thành công chiến lược "Phòng thủ theo chiều sâu": Kết hợp Permission Boundary (chặn leo thang quyền) và IAM Role Conditions (giới hạn theo IP/Thời gian) để đảm bảo nguyên tắc đặc quyền tối thiểu.
* Thiết lập hệ thống đánh giá an ninh tự động với AWS Security Hub, áp dụng các tiêu chuẩn quốc tế (CIS, PCI DSS) để phát hiện lỗ hổng cấu hình theo thời gian thực.
* Nâng cấp quy trình bảo vệ dữ liệu: Không chỉ sao lưu định kỳ với AWS Backup mà còn tích hợp AWS Lambda để tự động hóa việc kiểm thử khả năng khôi phục (Restore Test).

### Khó khăn – Giải pháp:
* User `ec2-admin` dù được gán quyền `AdministratorAccess` nhưng vẫn bị từ chối (Access Denied) khi thao tác tạo Instance
    * **Giải pháp:** Rà soát lại cơ chế Permission Boundary. Nhận ra quyền hiệu lực là "phép giao" (Intersection) giữa Policy gán cho user và Boundary. Đã điều chỉnh lại điều kiện `StringEquals` trong file JSON của Boundary để khớp với Region hiện tại.
* Gặp lỗi khi thực hiện Switch Role từ User thường sang Role quản trị (Trust Relationship Error)
    * **Giải pháp:** Kiểm tra lại tab Trust Relationships của Role. Cần khai báo chính xác ARN của User (Principal) vào Trust Policy thì AWS STS mới chấp nhận yêu cầu Assume Role.
* AWS Security Hub gửi quá nhiều cảnh báo (Findings) khiến việc lọc thông tin quan trọng gặp khó khăn
    * **Giải pháp:** Thực hiện tinh chỉnh (Tuning) bằng cách chuyển trạng thái các quy tắc không phù hợp với môi trường Lab sang `Suppressed` (Vô hiệu hóa) để giảm nhiễu.

### Bài học rút ra:
* Identity là vành đai bảo mật mới
    * Trong Cloud, Firewall là chưa đủ. Việc kiểm soát chặt chẽ Identity (Ai) và Permission (Được làm gì) mới là chốt chặn quan trọng nhất để bảo vệ tài nguyên.
* Backup phải đi đôi với Restore Test
    * Một bản sao lưu chưa từng được thử khôi phục thì hoàn toàn vô nghĩa. Việc tự động hóa quy trình Restore ngay sau khi Backup là tiêu chuẩn vàng (Gold Standard) cho tính sẵn sàng dữ liệu.
* Cấp quyền dựa trên ngữ cảnh (Context-aware Access)
    * Thay vì cấp quyền vĩnh viễn (Long-term credentials), ưu tiên sử dụng IAM Role với các điều kiện ràng buộc (Conditions) như địa chỉ IP nguồn hoặc khung giờ làm việc để giảm thiểu rủi ro khi lộ credentials.