---
title: "Worklog Tuần 8"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu tuần 8:
* **Làm chủ quy trình CI/CD cho Serverless:** Thiết kế và triển khai thành công pipeline tự động hóa hoàn toàn (End-to-End) cho ứng dụng Full-stack, tích hợp Gitlab với hệ sinh thái AWS CodeSuite (CodePipeline, CodeBuild) và CloudFormation.
* **Xây dựng Data Lake hiện đại & Tối ưu hóa Big Data:** Thực hiện trọn vẹn quy trình xử lý dữ liệu từ thu thập (Ingestion), làm sạch (DataBrew), chuyển đổi ETL sang định dạng Parquet (Glue) đến phân tích truy vấn (Athena) và trực quan hóa (QuickSight).
* **Củng cố tư duy kiến trúc & Hoàn thành đánh giá:** Hệ thống hóa kiến thức về AWS Well-Architected Framework (tập trung vào Performance & Cost Optimization) và hoàn thành bài thi giữa kỳ (Mid-term Exam) để kiểm chứng năng lực thiết kế hệ thống thực tế.


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | CHỦ ĐỀ: TRIỂN KHAI CI/CD CHO ỨNG DỤNG SERVERLESS VỚI AWS CODEPIPELINE <br> - **Lý thuyết:** <br>  + Tìm hiểu kiến trúc Serverless CI/CD: Tự động hóa quy trình Build, Package và Deploy ứng dụng Full-stack. <br>  + Cơ chế AWS SAM Pipelines: Bootstrap pipeline đa nền tảng (Gitlab, Jenkins, CodePipeline). <br>  + Các dịch vụ CodeSuite: CodePipeline (điều phối), CodeBuild (biên dịch), CloudFormation (IaC). <br> - **Thực hành:** <br>  + Setup môi trường: Cấu hình IAM Roles tuân thủ nguyên tắc Least Privilege. <br>  + Backend Pipeline: Tạo Gitlab Repo, cấu hình `buildspec.yml` và kết nối pipeline triển khai SAM Template. <br>  + Frontend Pipeline: Cập nhật API Endpoint, cấu hình auto-deploy artifacts ReactJS/VueJS lên S3 bucket. <br>  + Integration Test: Kiểm thử luồng hoạt động End-to-End (Register -\> Login -\> Create Book) tích hợp Cognito. | 27/10/2025 | 27/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | CHỦ ĐỀ: XÂY DỰNG DATA LAKE TRÊN AWS <br> - **Lý thuyết:** <br>  + Khái niệm Data Lake trên S3: Lưu trữ tập trung dữ liệu thô (Raw) và dữ liệu đã xử lý (Processed). <br>  + Hệ sinh thái AWS Glue: Crawler (khám phá schema), Data Catalog (quản lý metadata) và ETL Jobs. <br>  + Hiệu năng: So sánh định dạng Row-based (CSV) và Columnar (Parquet) trong truy vấn Big Data. <br> - **Thực hành:** <br>  + Ingestion & Prep: Khởi tạo Cloud9, kiểm tra encoding và upload dataset (Airbnb) lên S3. <br>  + Data Cleaning: Sử dụng Glue DataBrew (No-code) để profile dữ liệu, làm sạch và chuẩn hóa schema. <br>  + ETL Transformation: Viết Glue Job (Spark/Python) chuyển đổi CSV sang Parquet, thực hiện Partitioning tối ưu chi phí. <br>  + Analytics & BI: Truy vấn SQL tương tác với Amazon Athena và trực quan hóa dữ liệu trên QuickSight (Pie Chart, Scatter Plot). | 28/10/2025 | 28/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | CHỦ ĐỀ: THIẾT KẾ KIẾN TRÚC HIỆU NĂNG CAO (HIGH-PERFORMING ARCHITECTURES) <br> - **Ôn tập kiến thức:** <br>  + Compute Scaling: Cơ chế co giãn của EC2 Auto Scaling, Lambda concurrency và Fargate. <br>  + Storage Performance: Tối ưu hóa IOPS cho EBS, throughput cho EFS và các lớp lưu trữ S3. <br>  + Network Optimization: Giảm độ trễ (latency) với CloudFront (CDN) và AWS Global Accelerator. <br>  + Database Caching: Chiến lược caching với ElastiCache và DAX. <br> - **Chuẩn bị:** <br>  + Rà soát các chỉ số CloudWatch Metrics quan trọng để kích hoạt Scaling policy hiệu quả. | 29/10/2025 | 29/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | CHỦ ĐỀ: THIẾT KẾ TỐI ƯU CHI PHÍ (COST-OPTIMIZED ARCHITECTURES) <br> - **Ôn tập kiến thức:** <br>  + Cost Management: Phân tích chi phí với Cost Explorer và thiết lập cảnh báo ngân sách với AWS Budgets. <br>  + Pricing Models: So sánh và lựa chọn giữa On-Demand, Savings Plans và Spot Instances. <br>  + Storage Optimization: Thiết lập S3 Lifecycle Policies để tự động chuyển lớp lưu trữ (Tiering). <br>  + Network Costs: Tối ưu chi phí truyền tải dữ liệu qua NAT Gateway và VPC Peering. <br> - **Chuẩn bị:** <br>  + Review các kịch bản gắn thẻ phân bổ chi phí (Cost allocation tags). | 30/10/2025 | 30/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | CHỦ ĐỀ: THỰC HIỆN BÀI THI GIỮA KỲ (MID-TERM EXAM) <br> - **Nội dung thi:** <br>  + Secure Architectures: IAM, MFA, KMS Encryption, Security Groups, NACLs, WAF, Shield. <br>  + Resilient Architectures: Multi-AZ, Multi-Region, DR Strategies, Route 53. <br>  + High-Performing & Cost-Optimized: Các kiến trúc đã ôn tập trong tuần. <br>  + Well-Architected Framework: Áp dụng 6 trụ cột vào thiết kế hệ thống thực tế. <br> - **Hoạt động:** <br>  + Hoàn thành bài thi trắc nghiệm và thực hành Lab. <br>  + Tổng kết kết quả và xác định các lỗ hổng kiến thức cần cải thiện. | 31/10/2025 | 31/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Kết quả đạt được tuần 8:
* **Triển khai thành công hệ thống CI/CD Serverless tự động hóa hoàn toàn:** Tích hợp Gitlab với AWS CodePipeline để build Backend (SAM/CloudFormation) và deploy Frontend (S3 Static Website) thông qua file cấu hình `buildspec.yml`.
* **Xây dựng quy trình Data Lake chuẩn công nghiệp trên S3:** Vận dụng thành thạo AWS Glue Crawler để tự động nhận diện schema, sử dụng Glue DataBrew để làm sạch dữ liệu và Glue Jobs để thực hiện ETL.
* **Tối ưu hóa hiệu năng truy vấn Big Data:** Thực chứng và so sánh được hiệu quả vượt trội của định dạng Parquet (Columnar) so với CSV (Row-based) khi truy vấn bằng Amazon Athena (tốc độ nhanh hơn, chi phí quét thấp hơn ~10 lần).
* **Hệ thống hóa tư duy kiến trúc AWS (Well-Architected):** Nắm vững chiến lược Auto Scaling (phân biệt Dynamic vs Predictive Scaling) và các mô hình tối ưu chi phí lưu trữ (S3 Lifecycle Policies, Savings Plans) để chuẩn bị cho kỳ thi giữa kỳ.

### Khó khăn – Giải pháp:
* Lỗi kết nối API (Network Error) giữa Frontend và Backend sau khi deploy pipeline xong
  * *Giải pháp:* Kiểm tra lại file cấu hình Frontend. Cần lấy `ApiUrl` từ phần Output của CloudFormation Stack (Backend), cập nhật vào file `src/config.js`, và commit lại code để pipeline thực hiện build lại bản mới.

* AWS Glue Crawler nhận diện sai kiểu dữ liệu (Data Type) hoặc lỗi encoding ký tự
  * *Giải pháp:* Sử dụng AWS Glue DataBrew để chạy Profile job kiểm tra chất lượng dữ liệu trước. Dùng công cụ `enca` trên môi trường Cloud9 để chuẩn hóa encoding về UTF-8 cho các file CSV trước khi đưa vào pipeline xử lý.

* CodeBuild gặp lỗi "Access Denied" khi cố gắng đẩy artifacts lên S3 Bucket
  * *Giải pháp:* Rà soát IAM Role gán cho CodeBuild Project. Bổ sung quyền `s3:PutObject` cho đúng resource ARN của bucket đích (tuân thủ nguyên tắc Least Privilege) thay vì cấp quyền Admin quá rộng.

### Bài học rút ra:
* Sức mạnh của định dạng dữ liệu (Data Format Matters)
  * Trong xử lý Big Data trên Cloud, việc chuyển đổi dữ liệu sang định dạng cột (như Parquet) không chỉ là kỹ thuật mà là chiến lược tối ưu chi phí cốt lõi ("scan ít hơn nghĩa là trả tiền ít hơn").

* Tự động hóa là chìa khóa của sự ổn định (Automation for Stability)
  * CI/CD Pipeline không chỉ giúp deploy nhanh mà giúp loại bỏ hoàn toàn sai sót của con người (human errors). Đầu tư thời gian viết `buildspec.yml` chuẩn ngay từ đầu sẽ tiết kiệm thời gian debug vận hành về sau.

* Tư duy thiết kế "Design for Failure"
  * Mọi thành phần hạ tầng đều có thể gặp sự cố. Do đó, kiến trúc hệ thống luôn phải tách rời (Decoupled), triển khai đa vùng (Multi-AZ) và có cơ chế tự phục hồi (Auto Scaling) thay vì phụ thuộc vào một node duy nhất.