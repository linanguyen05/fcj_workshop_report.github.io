---
title: "Worklog Tuần 10"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:
* Hiểu tường tận kiến trúc Serverless RAG: Phân tích luồng dữ liệu và cơ chế tích hợp giữa API Gateway, AWS Lambda và Amazon Bedrock để xây dựng ứng dụng GenAI.
* Vận dụng kỹ thuật Data Engineering cho AI: Thực hiện chiến lược Semantic Chunking (phân đoạn ngữ nghĩa) và chuẩn hóa Metadata Schema để xử lý dữ liệu đa cấu trúc (Multi-domain).
* Triển khai hạ tầng Vector Database bảo mật: Cấu hình Amazon RDS (PostgreSQL) với extension pgvector và thiết lập Security Group đảm bảo kết nối nội bộ an toàn trong VPC.
* Quản trị và tích hợp Foundation Models: Nắm vững quy trình Request Model Access và sử dụng SDK (boto3) để tương tác hiệu quả với các model Cohere Embed và Claude 3 Sonnet.

### Các công việc cần triển khai trong tuần này:
Dưới đây là bảng worklog Tuần 10 đã được thiết kế lại hoàn toàn theo phong cách bạn yêu cầu: chuyên nghiệp, cô đọng, đúng cú pháp Markdown và phản ánh chính xác các đầu việc kỹ thuật về dự án RAG Tâm linh chúng ta đã thảo luận.

Cột "Nguồn tài liệu" đã được cập nhật thành tài liệu kỹ thuật chung và tài liệu nội bộ dự án thay vì link cũ.

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :------- | :-------- | :------ | :-------- |
| 2 | CHỦ ĐỀ: THIẾT KẾ KIẾN TRÚC RAG & QUY HOẠCH DỮ LIỆU ĐA LĨNH VỰC <br>- **Nghiên cứu lý thuyết:** <br>  + Phân tích luồng dữ liệu kiến trúc Serverless RAG: User Request -\> API Gateway -\> Lambda -\> Amazon Bedrock (Knowledge Base). <br>  + Thiết kế Data Schema cho hệ thống đa tác vụ (Multi-domain): Tích hợp Chiêm tinh (Astrology), Tarot và Thần số học vào chung một Vector Store. <br>- **Thực hành:** <br>  + Khởi tạo môi trường: Setup IAM Role cho Lambda (quyền truy cập RDS, Bedrock) và cấu hình VPC Network. <br>  + Lập kế hoạch Ingestion: Định nghĩa cấu trúc Metadata chuẩn (Category, Sub-category) để tối ưu khả năng lọc (Filtering) sau này. | 10/11/2025 | 10/11/2025 | AWS Documentation & Tài liệu dự án |
| 3 | CHỦ ĐỀ: XỬ LÝ DỮ LIỆU (DATA ENGINEERING) & MODULE HÓA CODE <br>- **Tối ưu hóa mã nguồn (Refactoring):** <br>  + Chuyển đổi code xử lý dữ liệu từ dạng nguyên khối (Monolithic) sang dạng Module: Tách biệt logic `config_mapping.py` (Business Logic) và `run_tagger.py` (Execution). <br>- **Thực hành:** <br>  + Metadata Tagging: Chạy script tự động gán thẻ phân loại cho 65 tài liệu gốc (Zodiac, Planets). <br>  + Debugging Logic: Xử lý các trường hợp ngoại lệ (Edge cases) khi map URL vào danh mục, đảm bảo độ chính xác 100% cho dataset. | 11/11/2025 | 11/11/2025 | AWS Python SDK (Boto3) Docs |
| 4 | CHỦ ĐỀ: CHIẾN LƯỢC PHÂN ĐOẠN (SEMANTIC CHUNKING) & MỞ RỘNG DOMAIN <br>- **Nghiên cứu:** <br>  + So sánh hiệu quả giữa Fixed-size Chunking và Semantic Chunking (dựa trên ngữ nghĩa/từ khóa) đối với dữ liệu tâm linh. <br>  + Chiến lược mở rộng Dataset: Phân tích cấu trúc file `cards.jsonl` (Tarot) để tích hợp vào hệ thống. <br>- **Thực hành:** <br>  + Data Transformation: Viết script chuẩn hóa dữ liệu Tarot về dạng `content` + `metadata` đồng bộ với Chiêm tinh. <br>  + Cập nhật `run_chunker.py` v2.1: Implement logic Regex và Fallback (RecursiveSplitter) để xử lý văn bản phức tạp. | 12/11/2025 | 12/11/2025 | LangChain Documentation |
| 5 | CHỦ ĐỀ: TRIỂN KHAI LAMBDA RAG & QUẢN TRỊ MODEL ACCESS <br>- **Triển khai Backend (Lambda):** <br>  + Implement hàm `get_embedding`: Tích hợp model **Cohere Embed v3** để vector hóa truy vấn. <br>  + Implement hàm `query_llm`: Tích hợp model **Claude 3 Sonnet** để sinh câu trả lời tự nhiên. <br>- **Thực hành & Debug:** <br>  + Xử lý lỗi `ValidationException`: Thực hiện quy trình "Request Model Access" cho các model của Anthropic tại region Singapore (ap-southeast-1). <br>  + Kiểm tra kết nối VPC: Đảm bảo Lambda trong VPC có thể kết nối tới RDS (PostgreSQL) qua Security Group. | 13/11/2025 | 13/11/2025 | AWS Bedrock User Guide |
| 6 | CHỦ ĐỀ: TỐI ƯU HÓA PAYLOAD & KIỂM THỬ HỆ THỐNG (END-TO-END) <br>- **Tối ưu hóa API Interface:** <br>  + Thiết kế lại cấu trúc JSON Payload: Chuyển sang dạng Nested Object (Lồng nhau) tách biệt `user_profile` (ngày/giờ sinh) và `input_data` để hỗ trợ cá nhân hóa sâu. <br>- **Thực hành:** <br>  + Setup Local Testing: Cấu hình `curl` scripts để giả lập request từ Frontend gọi vào API Gateway. <br>  + System Test: Chạy kiểm thử luồng RAG hoàn chỉnh (Ingestion -\> Retrieval -\> Generation) và verify độ chính xác của câu trả lời. | 14/11/2025 | 14/11/2025 | Tài liệu kỹ thuật dự án |


### Kết quả đạt được tuần 10:
* **Thiết kế thành công Data Schema đa lĩnh vực:** Đã chuẩn hóa dữ liệu từ các nguồn khác nhau (JSONL Tarot, Scraped Web) về định dạng `content` + `metadata` thống nhất, tạo tiền đề vững chắc cho việc mở rộng dataset sang Thần số học và Tử vi.
* **Làm chủ kỹ thuật Data Engineering cho RAG:** Chuyển đổi thành công mã nguồn xử lý dữ liệu từ dạng nguyên khối sang dạng Module (Module hóa), đồng thời áp dụng phương pháp "Semantic Chunking" (Phân đoạn ngữ nghĩa) giúp cải thiện độ chính xác của ngữ cảnh khi truy vấn.
* **Triển khai kiến trúc Serverless RAG hoàn chỉnh:** Đã tích hợp thành công hai mô hình AI trên Amazon Bedrock: Cohere Embed v3 (Vector hóa) và Claude 3 Sonnet (Sinh lời khuyên), kết nối bảo mật với RDS PostgreSQL thông qua VPC.
* **Tối ưu hóa Payload API:** Nâng cấp cấu trúc dữ liệu đầu vào (Input Payload) sang dạng Nested Object, cho phép hệ thống xử lý song song thông tin User Profile (ngày giờ sinh) để cá nhân hóa câu trả lời.

### Khó khăn – Giải pháp:
* Lỗi `ValidationException` khi gọi model Claude 3 Sonnet qua boto3 mặc dù code đúng logic
    * **Giải pháp:** Thực hiện quy trình "Request Model Access" thủ công trong Bedrock Console. Cần lưu ý cấp quyền cụ thể cho từng Model Family tại đúng Region đang triển khai (Singapore/ap-southeast-1).

* Dữ liệu Tarot (cấu trúc nhiều trường nhỏ) không tương thích với Schema của Chiêm tinh (văn bản dài)
    * **Giải pháp:** Xây dựng script Data Transformation (ETL) để gộp các trường dữ liệu con (`meaning`, `love`, `career`) thành một trường `content` giàu ngữ nghĩa trước khi thực hiện Embedding.

* Lambda bị Timeout khi cố gắng kết nối tới RDS Database để truy vấn Vector
    * **Giải pháp:** Cấu hình lại Security Group. Thay đổi Inbound Rule của RDS để chấp nhận traffic từ Security Group ID của Lambda thay vì IP cụ thể, đảm bảo kết nối nội bộ thông suốt trong VPC.

### Bài học rút ra:
* **Tư duy "Schema-First" trong hệ thống Multi-domain**
    * Trong bài toán RAG đa tác vụ, việc thiết kế Metadata (Category, Sub-category) quan trọng hơn việc chọn Model. Metadata càng chi tiết và chuẩn hóa thì khả năng lọc nhiễu (Filtering) và độ chính xác của câu trả lời càng cao.

* **Chất lượng Chunking quyết định độ thông minh của RAG**
    * Đối với dữ liệu đặc thù (Tâm linh/Văn học), kỹ thuật Regex-based Splitting (tách theo từ khóa/tiêu đề) hiệu quả hơn hẳn so với việc cắt đoạn theo ký tự cố định. Đầu tư vào khâu tiền xử lý (Preprocessing) mang lại lợi ích lớn hơn nhiều so với việc cố gắng tinh chỉnh Prompt (Prompt Engineering).