---
title: "Worklog Tuần 12"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---

### Mục tiêu tuần 12:
* Hiểu và thực hiện chuyển đổi kiến trúc từ mô hình truyền thống (RDS/VPC) sang kiến trúc Serverless thuần túy (No-VPC) để tối ưu hóa chi phí vận hành.
* Triển khai thành công luồng xử lý dữ liệu AI (RAG Pipeline) kết hợp Vector Database (Pinecone) và Key-Value Store (DynamoDB) thay thế cho SQL.
* Nắm vững kỹ thuật Refactoring Code cho AWS Lambda: Chuyển đổi từ `psycopg2` sang `boto3`, quản lý kết nối và xử lý Cold Start.
* Xây dựng tư duy "Monitoring as Code": Tự động hóa việc thiết lập cảnh báo lỗi và hiệu năng cho hệ thống bằng CloudWatch và Scripting.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :------- | :----------- | :-------------- | :------------- |
| 2 | CHỦ ĐỀ: THIẾT KẾ KIẾN TRÚC RAG & VECTOR DATABASE <br> - Nghiên cứu giải pháp AI/ML: <br>  + Phân tích mô hình **RAG (Retrieval-Augmented Generation)** để tối ưu hóa câu trả lời của AI dựa trên dữ liệu riêng. <br>  + Tìm hiểu về **Vector Database (Pinecone)** và mô hình Embedding (`cohere.embed-multilingual-v3.0`). <br> - **Thực hành:** <br>  + Khởi tạo Pinecone Index: Cấu hình tên `metaphysical-index`, Dimension `1024`, Metric `Cosine` phù hợp với model Cohere. <br>  + Chuẩn bị môi trường: Cài đặt các thư viện `pinecone-client`, `langchain` cho môi trường phát triển cục bộ. | 24/11/2025 | 24/11/2025 | |
| 3 | CHỦ ĐỀ: MIGRATION DỮ LIỆU - TỪ SQL SANG NOSQL & VECTOR <br> - Chiến lược chuyển đổi dữ liệu (ETL Strategy): <br>  + Thiết kế bảng **Amazon DynamoDB** (On-demand capacity) thay thế cho RDS PostgreSQL để tăng tốc độ truy xuất key-value. <br>  + Quy hoạch luồng dữ liệu: Metadata lưu tại DynamoDB, Vector Embeddings lưu tại Pinecone. <br> - **Thực hành:** <br>  + Tạo bảng DynamoDB `MetaphysicalKnowledgeBase`. <br>  + Viết Script ETL: Chuyển đổi dữ liệu từ `dataset_v3.jsonl` và RDS cũ -\> thực hiện Embedding -\> Upsert vào Pinecone và DynamoDB. <br>  + Xử lý sự cố: Debug và sửa lỗi sai lệch ID (ID Mismatch) giữa Pinecone vector và DynamoDB item. | 25/11/2025 | 25/11/2025 | |
| 4 | CHỦ ĐỀ: LAMBDA REFACTORING - TỐI ƯU HÓA BACKEND PYTHON <br> - Kỹ thuật lập trình Serverless: <br>  + Chuyển đổi tư duy code từ stateful (SQL connection pool) sang stateless (HTTP API calls với Boto3). <br>  + Tối ưu hóa cold-start bằng cách quản lý biến Global và Init context. <br> - **Thực hành:** <br>  + Refactor Code: Viết lại toàn bộ Lambda Function xử lý logic "Tarot/Horoscope". Loại bỏ thư viện `psycopg2` (RDS), thay thế bằng `boto3` (DynamoDB). <br>  + Tích hợp Bedrock: Cấu hình logic gọi model Claude 3 Sonnet kết hợp context lấy từ Pinecone (RAG Flow). <br>  + Debugging: Xử lý các lỗi runtime liên quan đến thư viện và quyền IAM. | 26/11/2025 | 26/11/2025 | |
| 5 | CHỦ ĐỀ: INFRASTRUCTURE MODERNIZATION - CHUYỂN ĐỔI NO-VPC <br> - Tối ưu hóa hạ tầng và chi phí (Cost Optimization): <br>  + Phân tích lợi ích của kiến trúc **Lambda No-VPC**: Loại bỏ thời gian chờ tạo ENI, loại bỏ chi phí NAT Gateway đắt đỏ. <br>  + Đánh giá bảo mật khi chuyển sang public endpoint với IAM Auth. <br> - **Thực hành:** <br>  + Cấu hình mạng: Gỡ bỏ cấu hình VPC subnet/security group khỏi Lambda Function. <br>  + Dọn dẹp tài nguyên (Cleanup): Terminate RDS Instance, xóa VPC Endpoints và NAT Gateway cũ. <br>  + Kiểm thử hệ thống: Verify lại toàn bộ tính năng sau khi "cắt" VPC để đảm bảo độ trễ (latency) giảm và kết nối ổn định. | 27/11/2025 | 27/11/2025 | |
| 6 | CHỦ ĐỀ: MONITORING STRATEGY - GIÁM SÁT TỰ ĐỘNG HÓA <br> - Chiến lược vận hành (Operational Excellence): <br>  + Xác định các "Golden Signals" cần giám sát cho Serverless: Errors, Throttles, Duration và Concurrent Executions. <br>  + Tư duy "Monitoring as Code": Sử dụng script thay vì thao tác tay (ClickOps). <br> - **Thực hành:** <br>  + CloudWatch Automation: Sử dụng **AWS CloudShell** viết script Bash/CLI để tự động tạo Alarm cho tất cả Lambda Functions. <br>  + Thiết lập cảnh báo: Cấu hình ngưỡng (Threshold) cho Error Rate \> 1% và Duration \> 25s (tránh timeout API Gateway). <br>  + Nghiệm thu: Kiểm tra luồng gửi mail cảnh báo qua SNS khi cố tình trigger lỗi giả lập. | 28/11/2025 | 28/11/2025 | |


### Kết quả đạt được tuần 12:
* **Hiện đại hóa kiến trúc (Modernization):** Hoàn tất chuyển đổi hệ thống sang kiến trúc **Serverless thuần túy (No-VPC)**. Kết quả giúp loại bỏ hoàn toàn chi phí cố định của NAT Gateway/RDS, đưa chi phí hạ tầng về mức tối thiểu (~0$ khi không có traffic).
* **Triển khai RAG Pipeline:** Xây dựng thành công luồng xử lý dữ liệu AI lai ghép: Sử dụng **Pinecone** cho tìm kiếm ngữ nghĩa (Semantic Search) và **DynamoDB** cho truy xuất Metadata tốc độ cao, thay thế hoàn toàn truy vấn SQL phức tạp.
* **Tự động hóa vận hành:** Thay vì thao tác tay (ClickOps), đã xây dựng được bộ script chạy trên **AWS CloudShell** để tự động thiết lập CloudWatch Alarms cho toàn bộ Lambda Function, đảm bảo khả năng giám sát hệ thống tức thì.
* **Tối ưu hóa hiệu năng (Performance):** Giảm độ trễ (Latency) của ứng dụng bằng cách gỡ bỏ Lambda khỏi VPC (loại bỏ thời gian khởi tạo ENI) và chuyển đổi logic kết nối Database từ `psycopg2` sang `boto3`.

### Khó khăn – Giải pháp:
* Mất đồng bộ dữ liệu (Data Consistency) giữa Vector DB và NoSQL DB (lỗi ID mismatch) dẫn đến AI truy xuất sai ngữ cảnh
  * Giải pháp: Viết lại quy trình ETL, thực hiện chuẩn hóa ID ngay từ bước tiền xử lý (Preprocessing) trước khi đẩy vào cả hai cơ sở dữ liệu và debug từng bước (step-by-step).

* Lambda gặp lỗi Timeout và Cold Start cao khi khởi tạo kết nối đến Bedrock và Pinecone
  * Giải pháp: Tối ưu hóa code Python bằng cách đưa việc khởi tạo Client (Pinecone, Boto3) ra ngoài `handler` (tận dụng Global Scope/Init Phase). Điều chỉnh tăng cấu hình Timeout và Memory cho Lambda.

### Bài học rút ra:
* **Tư duy "Cost-Effective Architecture"**
  * Không phải lúc nào đặt Lambda trong VPC cũng tốt. Hiểu rõ sự đánh đổi giữa bảo mật mạng (Private Subnet) và chi phí/hiệu năng. Với các ứng dụng sử dụng Managed Services (DynamoDB, Bedrock), kiến trúc **No-VPC** là lựa chọn tối ưu để loại bỏ chi phí NAT Gateway.

* **Chuyển đổi tư duy dữ liệu (SQL to NoSQL)**
  * Hiểu sự khác biệt cốt lõi giữa thiết kế chuẩn hóa (RDS) và thiết kế theo Access Patterns (DynamoDB). Dữ liệu cần được phi chuẩn hóa (Denormalization) để tối ưu tốc độ đọc cho ứng dụng Real-time AI.

* **Monitoring as Code**
  * Việc thiết lập Monitoring/Alarm phải được thực hiện song song với việc phát triển tính năng (Dev + Ops) và nên sử dụng Script/IaC thay vì thao tác thủ công để quản lý số lượng lớn resources.