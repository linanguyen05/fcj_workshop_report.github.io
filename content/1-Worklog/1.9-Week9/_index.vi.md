---
title: "Worklog Tuần 9"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:
* Xây dựng hệ thống Data Lake Serverless hoàn chỉnh trên S3: Từ thu thập (Ingest), lưu trữ, làm sạch (ETL) đến phân tích và trực quan hóa dữ liệu.
* Thành thạo các công cụ xử lý dữ liệu lớn (Big Data): Vận dụng AWS Glue (DataBrew, Crawler, Job) để chuẩn hóa dữ liệu và Amazon Athena/Redshift để truy vấn phân tích.
* Trực quan hóa dữ liệu kinh doanh (BI): Thiết kế Dashboard tương tác, áp dụng ML Insights và dự báo (Forecast) với Amazon QuickSight.
* Tối ưu hóa chi phí AWS (FinOps): Nắm vững mô hình phân tích chi phí (Cost Explorer), phí truyền tải dữ liệu (Data Transfer) và các chiến lược cam kết sử dụng (Savings Plans, Reserved Instances).


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | -------- | -------- | -------- | -------- |
| 2 | CHỦ ĐỀ: XÂY DỰNG DATA LAKE TRÊN S3 & CHUẨN BỊ DỮ LIỆU <br>- Lý thuyết nền tảng & Kiến trúc: <br>  + Hiểu vai trò của Amazon S3 làm Central Data Lake và tầm quan trọng của UTF-8 Encoding. <br>  + Nắm vững AWS Glue DataBrew (Data Profiling, Recipe) để làm sạch dữ liệu without-code. <br>  + Phân biệt định dạng lưu trữ hàng (CSV) và cột (Parquet) để tối ưu hiệu năng truy vấn. <br>- **Thực hành:** <br>  + Setup môi trường: Khởi tạo Cloud9, cài đặt tool `enca`, upload dữ liệu thô (Raw Data) lên S3. <br>  + Data Preparation: Cấu hình DataBrew Project để profile, làm sạch và chuẩn hóa dữ liệu Airbnb. <br>  + Catalog & ETL: Chạy Glue Crawler tạo Metadata và thực thi Glue Job chuyển đổi định dạng CSV sang Parquet. | 03/11/2025 | 03/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | CHỦ ĐỀ: XÂY DỰNG PIPELINE PHÂN TÍCH DỮ LIỆU (INGEST-TRANSFORM-ANALYZE) <br>- Kiến trúc Analytics End-to-End: <br>  + Quy trình dòng chảy dữ liệu: Kinesis (Ingest) -\> S3 (Store) -\> Glue/EMR (Transform) -\> Athena/Redshift (Analyze). <br>  + So sánh các phương pháp ETL: Glue Studio (Visual), Glue Notebook (Code) và DataBrew. <br>  + Kiến trúc Data Warehouse (Redshift) và Serverless Serving (Lambda). <br>- **Thực hành:** <br>  + Streaming Data: Cấu hình Kinesis Firehose nạp dữ liệu giả lập (KDG) vào S3 theo thời gian thực. <br>  + ETL Processing: Sử dụng Glue Studio để Join bảng và Glue Notebook (PySpark) để xử lý dữ liệu phức tạp. <br>  + Real-time & Warehousing: Chạy Flink SQL trên Kinesis Analytics và load dữ liệu vào cụm Redshift Cluster. | 04/11/2025 | 04/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | CHỦ ĐỀ: TRỰC QUAN HÓA DỮ LIỆU VỚI AMAZON QUICKSIGHT <br>- Tư duy thiết kế Dashboard & BI Serverless: <br>  + Cơ chế hoạt động của SPICE (in-memory engine) và mô hình Auto-scaling của QuickSight. <br>  + Các khái niệm cốt lõi: Dataset, Analysis, Dashboard và nguyên tắc phân chia Sheet/Theme. <br>- **Thực hành:** <br>  + Xây dựng Visuals: Kết nối Athena, tạo biểu đồ KPI, Line Chart, Donut Chart cho dữ liệu Sales. <br>  + Advanced Features: Ứng dụng ML Insights để tạo Forecast (dự báo) và Drill-down dữ liệu chi tiết. <br>  + Interactivity: Thiết lập bộ lọc xếp tầng (Cascading Filters), Navigation Actions và xuất bản (Publish) báo cáo. | 05/11/2025 | 05/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | CHỦ ĐỀ: GIÁM SÁT & QUẢN LÝ CHI PHÍ VỚI COST EXPLORER <br>- Nguyên lý quản trị tài chính Cloud: <br>  + Tổng quan về AWS Cost Explorer và chiến lược Tagging (Cost Allocation Tags). <br>  + Nắm rõ mô hình tính phí Data Transfer: Inbound (Free), Outbound và đặc biệt là phí Inter-AZ/Inter-Region. <br>- **Thực hành:** <br>  + Phân tích Resource: Kích hoạt Cost Explorer, lọc chi phí theo Service (EC2) và Tag để tìm điểm nóng ngân sách. <br>  + Audit Data Transfer: Phân tích chi phí truyền tải dữ liệu Outbound và giao tiếp giữa các AZ. <br>  + Reporting: Tạo và lưu các Custom Reports để theo dõi chi phí định kỳ hàng tháng. | 06/11/2025 | 06/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | CHỦ ĐỀ: CHIẾN LƯỢC TỐI ƯU CHI PHÍ (SAVINGS PLANS & RI) <br>- Các mô hình cam kết sử dụng (Commitment Models): <br>  + Phân biệt Savings Plans (Linh hoạt, áp dụng cho Fargate/Lambda) và Reserved Instances (Truyền thống). <br>  + So sánh EC2 Instance Savings Plans (Sâu) vs Compute Savings Plans (Rộng). <br>  + Đặc thù của Reserved DB Instances cho RDS (Ràng buộc Engine/Class). <br>- **Thực hành:** <br>  + Quy trình mua: Thao tác trên Console để xem Recommendations và thực hiện Purchase Savings Plans/RI. <br>  + Quản lý vòng đời: Tìm hiểu cách sử dụng Marketplace để mua/bán RI và kỹ thuật Queueing đơn hàng. <br>  + Tổng kết & Dọn dẹp tài nguyên toàn bộ Lab tuần 3. | 07/11/2025 | 07/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Kết quả đạt được tuần 9:
* **Xây dựng thành công kiến trúc Serverless Data Lake trên S3:** Hiểu và triển khai được quy trình phân tầng dữ liệu (Raw -> Cleaned -> Curated). Nắm bắt vai trò quan trọng của việc kiểm tra Encoding (UTF-8) bằng công cụ `enca` trên Cloud9 trước khi ingest dữ liệu.
* **Thành thạo quy trình ETL và tối ưu hiệu năng truy vấn:**
    * Vận dụng linh hoạt 3 phương pháp ETL: **AWS Glue DataBrew** (No-code cleaning), **Glue Studio** (Visual Join) và **Glue Notebook** (PySpark scripting).
    * Chứng minh được hiệu quả của định dạng **Parquet** (Columnar) so với CSV: giảm dung lượng lưu trữ, tăng tốc độ truy vấn Athena và giảm chi phí scan dữ liệu gấp nhiều lần.
* **Triển khai Pipeline phân tích Real-time & Visualization:**
    * Cấu hình thành công **Kinesis Firehose** để nạp luồng dữ liệu giả lập vào S3.
    * Xây dựng Dashboard tương tác trên **Amazon QuickSight**, ứng dụng bộ nhớ **SPICE** và các tính năng ML Insights (Forecast, Anomaly Detection).
* **Nắm vững chiến lược Quản trị & Tối ưu chi phí (FinOps):**
    * Sử dụng **Cost Explorer** để "soi" chi phí ở cấp độ Resource và phát hiện lãng phí từ phí Data Transfer (Inter-AZ).
    * Phân biệt rõ ràng tư duy chọn gói cam kết: Ưu tiên **Compute Savings Plans** cho sự linh hoạt (Compute/Lambda/Fargate) và **Reserved Instances** khi cần mức giảm giá sâu nhất cho hạ tầng ổn định (RDS/EC2).

### Khó khăn – Giải pháp:
* **Lỗi hiển thị ký tự lạ khi Crawler quét dữ liệu thô (Raw Data)**
    * **Giải pháp:** Dữ liệu gốc từ nhiều nguồn thường sai lệch bảng mã. Cần sử dụng lệnh `enca -L none` trên môi trường Linux (Cloud9) để phát hiện và convert toàn bộ file về chuẩn UTF-8 trước khi upload lên S3.

* **Chi phí Data Transfer tăng cao bất thường dù không tải dữ liệu ra Internet**
    * **Giải pháp:** Kiểm tra lại kiến trúc mạng. Phát hiện traffic giao tiếp giữa các EC2 Instance nằm khác Availability Zone (Inter-AZ Data Transfer). Giải pháp là quy hoạch lại resource về cùng 1 AZ nếu không yêu cầu HA quá khắt khe, hoặc sử dụng VPC Endpoints cho S3 để traffic đi trong mạng nội bộ AWS.

* **Athena scan quá nhiều dữ liệu gây chậm và tốn chi phí**
    * **Giải pháp:** Thay vì truy vấn trực tiếp file CSV (quét toàn bộ file), đã chuyển đổi dữ liệu sang định dạng **Parquet** kết hợp quy hoạch **Partitioning** (phân vùng thư mục theo thời gian). Kết quả giảm lượng dữ liệu quét xuống chỉ còn 1/10.

### Bài học rút ra:
* **Format:** Trong Big Data, cách lưu trữ quan trọng hơn nơi lưu trữ. Việc chuyển đổi sang định dạng cột (**Parquet/ORC**) và chiến lược phân vùng (**Partitioning**) là kỹ thuật bắt buộc để đảm bảo hiệu năng và chi phí thấp.
* **Tagging là xương sống của FinOps:** Cost Explorer sẽ trở nên vô dụng nếu tài nguyên thiếu **Tag**. Cần thiết lập kỷ luật gắn tag `Project`, `Environment`, `Owner` ngay từ khi tạo resource để minh bạch hóa bức tranh tài chính.
* **Chiến lược cam kết thông minh:** Đừng vội mua Reserved Instances (RI) nếu chưa chắc chắn về kiến trúc lâu dài. **Compute Savings Plans** là lựa chọn an toàn hơn vì nó giống như gói cước "trọn gói" (cho phép đổi từ EC2 sang Lambda/Fargate), trong khi RI giống như "đặt bàn cố định" (khó thay đổi).