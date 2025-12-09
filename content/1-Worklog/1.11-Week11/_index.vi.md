---
title: "Worklog Tuần 11"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:
* Hiểu sâu và vận dụng kỹ thuật "Semantic Chunking" (Phân đoạn ngữ nghĩa) để chuẩn hóa và tối ưu hóa dữ liệu đầu vào cho hệ thống RAG đa lĩnh vực (Chiêm tinh, Tarot).
* Làm chủ quy trình triển khai hạ tầng Serverless: Cấu hình AWS Lambda trong môi trường VPC, thiết lập IAM Roles và Security Groups để kết nối an toàn tới Amazon RDS và Amazon Bedrock.
* Thiết kế và triển khai RESTful API trên Amazon API Gateway với phương thức POST, xử lý các cấu trúc payload phức tạp (JSON lồng nhau) phục vụ tính năng cá nhân hóa.


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | **CHỦ ĐỀ: KIẾN TRÚC RAG MULTI-DOMAIN & CHUẨN HÓA DỮ LIỆU** <br>- **Nghiên cứu kiến trúc:** <br>  + Phân tích luồng dữ liệu cho hệ thống RAG đa lĩnh vực (Chiêm tinh, Tarot, Thần số học). <br>  + Đánh giá giải pháp lưu trữ Vector: Lựa chọn RDS (PostgreSQL với pgvector) thay vì DynamoDB để tối ưu truy vấn quan hệ kết hợp vector. <br>- **Thực hành:** <br>  + Refactor Code: Tái cấu trúc mã nguồn Python từ dạng Monolithic sang Modular (`config_mapping.py`, `run_tagger.py`) để dễ bảo trì. <br>  + Thiết kế Schema: Thống nhất định dạng dữ liệu đầu vào `content` + `metadata` cho cả dataset Tarot và Chiêm tinh. | 17/11/2025 | 17/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | **CHỦ ĐỀ: KỸ THUẬT DATA ENGINEERING & SEMANTIC CHUNKING** <br>- **Xử lý dữ liệu nâng cao:** <br>  + Hoàn thiện script `run_chunker.py` (v2.1): Tích hợp Regex (`re.IGNORECASE`) để nhận diện thực thể (Cung, Hành tinh) làm điểm ngắt ngữ nghĩa. <br>  + Xử lý ngôn ngữ tự nhiên: Implement hàm `slugify` để chuẩn hóa Metadata tiếng Việt (loại bỏ dấu, format chuẩn) phục vụ tìm kiếm chính xác. <br>- **Thực hành:** <br>  + Chạy tác vụ "Metadata Tagging" phân loại tài liệu vào danh mục (Zodiac, Planets). <br>  + Thực thi "Semantic Chunking" và Debug các lỗi logic khi mapping URL vào Category. | 18/11/2025 | 18/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | **CHỦ ĐỀ: INFRASTRUCTURE - LAMBDA TRONG VPC & BEDROCK SECURITY** <br>- **Kiến thức mạng AWS:** <br>  + Cơ chế định tuyến của Lambda trong VPC và kết nối tới RDS nằm ở Availability Zone khác (Multi-AZ). <br>  + Cấu hình Security Group Rule để cho phép traffic từ Lambda tới Database. <br>- **Thực hành:** <br>  + Deploy Lambda `metaphysicalAPI`: Cấu hình VPC, Subnet (Public-b) và IAM Role truy cập Bedrock. <br>  + Quản lý Model AI: Thực hiện "Request Access" cho model Claude 3 Sonnet và Cohere Embed tại region Singapore để khắc phục lỗi `ValidationException`. | 19/11/2025 | 19/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | **CHỦ ĐỀ: THIẾT KẾ RESTFUL API & CẤU TRÚC PAYLOAD PHỨC TẠP** <br>- **Thiết kế API Gateway:** <br>  + Khởi tạo REST API (`Metaphysical-Gateway`) với Endpoint Type là Regional. <br>  + Định nghĩa Resource `/metaphysical` và Method **POST** để bảo mật dữ liệu người dùng. <br>- **Thực hành:** <br>  + Xây dựng cấu trúc JSON Payload: Thiết kế Nested Object chứa `user_context` (ngày sinh, giờ sinh, nơi sinh) và `feature_type` để phục vụ tính năng cá nhân hóa câu trả lời. <br>  + Cấu hình Integration Request để chuyển tiếp dữ liệu vào Lambda. | 20/11/2025 | 20/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | **CHỦ ĐỀ: TÍCH HỢP HỆ THỐNG (INTEGRATION) & KIỂM THỬ** <br>- **Cấu hình & Bảo mật:** <br>  + Bật CORS (Cross-Origin Resource Sharing) trên API Gateway để cho phép Frontend gọi API. <br>  + Rà soát quyền IAM (Least Privilege) cho các service Lambda, Bedrock và RDS. <br>- **Thực hành:** <br>  + Local Testing: Thiết lập môi trường kiểm thử cục bộ, sử dụng `curl` và Postman để bắn request giả lập. <br>  + Kiểm thử luồng đi (End-to-End Test): Xác nhận dữ liệu đi từ API -\> Lambda -\> Bedrock -\> Trả về kết quả JSON đúng cấu trúc. | 21/11/2025 | 21/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |


### Kết quả đạt được tuần 11:
* **Hoàn thiện Pipeline xử lý dữ liệu RAG Đa lĩnh vực (Multi-domain):**
    * Đã giải quyết bài toán phân mảnh dữ liệu phức tạp bằng phương pháp "Semantic Chunking" (Phân đoạn ngữ nghĩa). Thay vì cắt văn bản máy móc, hệ thống giờ đây tự động nhận diện thực thể (Hành tinh, Cung hoàng đạo) để ngắt đoạn chính xác.
    * Chuẩn hóa thành công Schema dữ liệu đầu vào (`content` + `metadata`) cho cả hai tác vụ Tarot và Chiêm tinh, tạo tiền đề mở rộng sang Thần số học.
* **Triển khai hạ tầng Serverless kết nối AI:**
    * Xây dựng thành công RESTful API trên Amazon API Gateway, tích hợp chặt chẽ với AWS Lambda làm backend xử lý logic điều phối.
    * Cấu hình thành công kết nối an toàn giữa Lambda (trong Public Subnet) và RDS Database (trong Private Subnet) phục vụ lưu trữ Vector.
* **Tối ưu hóa mã nguồn (Refactoring):** Chuyển đổi toàn bộ mã nguồn xử lý dữ liệu từ dạng nguyên khối (Monolithic) sang dạng Module hóa (`config_mapping.py`, `run_chunker.py`), giúp code dễ đọc, dễ debug và dễ bảo trì hơn.

### Khó khăn – Giải pháp:
* **Lỗi `ValidationException` khi gọi model Anthropic Claude 3 trên Bedrock**
    * **Nguyên nhân:** Mặc định AWS không cấp quyền truy cập ngay lập tức vào các Model của bên thứ ba (như Anthropic, Cohere).
    * **Giải pháp:** Truy cập Bedrock Console, vào mục "Model access", chọn Region Singapore và thực hiện "Request access" thủ công cho từng model cụ thể (Claude 3 Sonnet, Cohere Embed).
* **Lambda bị Timeout khi cố gắng kết nối tới RDS**
    * **Nguyên nhân:** Lambda được đặt trong VPC nhưng Security Group của RDS chưa cho phép traffic đi vào từ Lambda.
    * **Giải pháp:** Thay vì mở IP (kém bảo mật), đã cấu hình Security Group của RDS để chấp nhận Inbound Rule với Source là **Security Group ID của Lambda**. Điều này tạo ra một "chuỗi tin cậy" (Chain of trust) nội bộ an toàn.
* **Dữ liệu Metadata tiếng Việt có dấu gây khó khăn cho việc tìm kiếm/lọc (Filtering)**
    * **Giải pháp:** Viết hàm tiện ích `slugify` (sử dụng thư viện `unicodedata`) để chuẩn hóa toàn bộ Metadata sang dạng không dấu, chữ thường và dùng gạch nối (ví dụ: "Bạch Dương" -> "bach-duong"), giúp OpenSearch/Postgres truy vấn chính xác tuyệt đối.

### Bài học rút ra:
* **Chất lượng Data quyết định chất lượng AI (Garbage In, Garbage Out)**
    * Kỹ thuật RAG không chỉ nằm ở việc chọn Model xịn, mà nằm ở khâu chuẩn bị dữ liệu (Data Preparation). Việc đầu tư thời gian vào Regex để cắt đoạn ngữ nghĩa (Semantic Chunking) mang lại hiệu quả tìm kiếm cao hơn nhiều so với việc cắt theo độ dài cố định.
* **Tư duy về Thiết kế API (RESTful Design)**
    * Với các payload phức tạp chứa thông tin ngữ cảnh người dùng (`user_context`), sử dụng phương thức **POST** là bắt buộc để đảm bảo tính bảo mật và khả năng mở rộng dữ liệu, thay vì cố nhồi nhét vào URL parameters của phương thức GET.
* **Cơ chế Networking trong VPC**
    * Hiểu rõ rằng các tài nguyên trong cùng một VPC (dù khác Subnet hay Availability Zone) vẫn có thể giao tiếp mượt mà nếu Route Table và Security Group được cấu hình đúng. Không nhất thiết phải đặt chung AZ mới kết nối được.