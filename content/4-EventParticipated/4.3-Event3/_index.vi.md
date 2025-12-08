---
title: "Event 3"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

### AWS Cloud Mastery Series #1: Workshop AI/ML/GenAI trên AWS

### Mục Đích Của Sự Kiện

Buổi workshop được tổ chức nhằm xóa nhòa khoảng cách giữa lý thuyết Machine Learning (ML) và ứng dụng thực tế trong doanh nghiệp. Trọng tâm của sự kiện là trang bị cho người tham dự tư duy "Cloud-native" khi xây dựng các giải pháp AI: từ việc chuẩn hóa quy trình ML truyền thống (MLOps) với **Amazon SageMaker** đến việc đón đầu làn sóng Generative AI (GenAI) thông qua **Amazon Bedrock**. Mục tiêu cuối cùng là giúp lập trình viên hiểu rõ cách tích hợp các mô hình ngôn ngữ lớn (LLMs) vào ứng dụng một cách an toàn, bảo mật và tối ưu chi phí.

### Tổng Quan Chương Trình

#### 8:30 – 9:00 | Chào Mừng & Bức Tranh Toàn Cảnh

  - Check-in và networking cùng các kỹ sư AWS cũng như cộng đồng developer.
  - Giới thiệu lộ trình workshop và định hướng tư duy giải quyết vấn đề bằng AI.
  - Cập nhật xu hướng AI/ML tại thị trường Việt Nam: Cơ hội và thách thức cho nhân sự trẻ.

#### 9:00 – 10:30 | Deep Dive: Hệ Sinh Thái ML Truyền Thống trên AWS

**Amazon SageMaker – Từ Dữ Liệu Thô đến Production:**

  - **Data Engineering:** Tiếp cận các công cụ như SageMaker Data Wrangler để làm sạch và visualize dữ liệu mà không cần viết quá nhiều code (low-code), kết hợp với Ground Truth để gán nhãn dữ liệu tự động.
  - **Training & Tuning:** Tìm hiểu cách SageMaker quản lý hạ tầng training (instance management), sử dụng Spot Instances để tiết kiệm chi phí và kỹ thuật Automatic Model Tuning để tìm bộ hyperparameters tối ưu.
  - **MLOps Best Practices:** Làm quen với SageMaker Pipelines và Model Registry để quản lý vòng đời mô hình, đảm bảo tính lặp lại (reproducibility) và tự động hóa quy trình CI/CD cho ML.

**Demo Trực Tiếp: Trải nghiệm SageMaker Studio**
Phần demo cho thấy sức mạnh của "Single Pane of Glass" (tất cả trên một giao diện) của SageMaker Studio, giúp developer chuyển đổi mượt mà giữa viết code trên Notebook, theo dõi experiment và deploy endpoint chỉ bằng vài cú click.

#### 10:45 – 12:00 | Kỷ Nguyên Generative AI với Amazon Bedrock

**Foundation Models (FMs) – Quyền Năng Của Sự Lựa Chọn:**

  - Tiếp cận khái niệm "Serverless GenAI": Sử dụng các mô hình hàng đầu (Claude 3.5 Sonnet, Llama 3, Amazon Titan) thông qua API duy nhất mà không cần quản lý server.
  - Phân tích chiến lược lựa chọn Model: Cân bằng giữa độ thông minh (Intelligence), tốc độ (Latency) và chi phí (Cost).

**Advanced Prompt Engineering & Reasoning:**

  - **Zero-shot vs Few-shot:** Kỹ thuật cung cấp ví dụ mẫu để định hướng câu trả lời của model.
  - **Chain-of-Thought (CoT):** Kỹ thuật "bẻ nhỏ" vấn đề phức tạp, giúp model suy luận logic hơn, đặc biệt hữu ích cho các bài toán toán học hoặc logic nghiệp vụ.

**RAG (Retrieval-Augmented Generation) & Knowledge Bases:**

  - Giải quyết vấn đề "ảo giác" (Hallucination) và dữ liệu lỗi thời của LLM bằng kiến trúc RAG.
  - Thực hành tích hợp Knowledge Base for Amazon Bedrock: Tự động hóa quy trình vectorization dữ liệu từ S3 vào Vector Store (như OpenSearch Serverless).

**Agents & Guardrails – Xây Dựng Ứng Dụng Thông Minh & An Toàn:**

  - **Agents:** Cách AI thực hiện hành động (gọi API, truy vấn database) thay vì chỉ trả lời văn bản.
  - **Guardrails:** Thiết lập "hàng rào bảo vệ" để lọc các nội dung độc hại, nhạy cảm hoặc không phù hợp với chính sách doanh nghiệp (PII redaction).

**Demo Trực Tiếp: Chatbot Trợ Lý Ảo Doanh Nghiệp**
Xây dựng một chatbot nội bộ có khả năng tra cứu tài liệu quy trình công ty (thông qua RAG) và từ chối trả lời các câu hỏi về tài chính nhạy cảm (nhờ Guardrails).

### Nội Dung Nổi Bật

  - **Tính thống nhất:** SageMaker không chỉ là công cụ training mà là một hệ sinh thái MLOps trọn vẹn.
  - **Dễ dàng tiếp cận GenAI:** Amazon Bedrock dân chủ hóa việc sử dụng các mô hình AI tiên tiến nhất thông qua API đơn giản.
  - **Sức mạnh của RAG:** Đây là "chìa khóa vàng" để đưa dữ liệu riêng (proprietary data) vào AI mà không cần fine-tune model tốn kém.
  - **Responsible AI:** An toàn dữ liệu và kiểm soát nội dung (Guardrails) là yếu tố bắt buộc (non-negotiable) khi đưa ứng dụng ra thực tế.

### Những Gì Tôi Học Được

  - **Tư duy về Hạ tầng:** Hiểu được sự khác biệt to lớn giữa việc chạy model ở local và chạy trên Cloud với khả năng scale linh hoạt.
  - **Context là Vua:** Trong GenAI, kỹ năng Prompt Engineering và việc cung cấp context đúng (qua RAG) quan trọng hơn việc cố gắng chỉnh sửa trọng số của model.
  - **Workflow tự động hóa:** SageMaker Studio giúp giảm thiểu các thao tác thủ công, cho phép developer tập trung vào logic thuật toán.
  - **Bảo mật từ thiết kế:** Việc tích hợp Guardrails ngay từ khâu thiết kế giúp tránh rủi ro pháp lý và thương hiệu sau này.

### Ứng Dụng Vào Công Việc

  - **Phân tích dữ liệu:** Đề xuất sử dụng SageMaker Studio Lab để thực hiện các bài toán phân tích dữ liệu quy mô nhỏ tại công ty/dự án cá nhân.
  - **Triển khai RAG:** Xây dựng một công cụ tìm kiếm nội bộ (Internal Search Tool) cho tài liệu kỹ thuật của team sử dụng Amazon Bedrock và Knowledge Base.
  - **Tối ưu quy trình:** Nghiên cứu sử dụng Bedrock Agents để tự động hóa các tác vụ lặp lại như tóm tắt báo cáo hàng tuần hoặc trích xuất thông tin từ hóa đơn.
  - **Chuẩn hóa Prompt:** Xây dựng thư viện Prompt Template chuẩn cho team để đảm bảo chất lượng output đồng nhất từ AI.

### Trải Nghiệm Cá Nhân

Đây thực sự là một buổi workshop bổ ích đối với một sinh viên thực tập như em. Trước đây, các thuật ngữ như RAG hay Vector Database thường khá trừu tượng trên lý thuyết, nhưng khi được trực tiếp thao tác trên Amazon Bedrock console, mọi thứ trở nên rõ ràng và logic hơn rất nhiều.

  - Em đặc biệt ấn tượng với tốc độ triển khai: chỉ mất khoảng 30 phút để dựng lên một chatbot có khả năng hiểu tài liệu PDF của riêng mình – điều mà nếu code thủ công sẽ mất nhiều ngày.
  - Giao diện trực quan của SageMaker Studio giúp em bớt "sợ" khi nghĩ đến việc quản lý hạ tầng cho ML.
  - Quan trọng nhất, em nhận ra rằng trong kỷ nguyên AI, kỹ năng "đặt câu hỏi" (Prompting) và tư duy hệ thống (System Design) đang trở nên quan trọng không kém gì kỹ năng coding thuần túy.

### Bài Học Rút Ra

  - **Dữ liệu là nhiên liệu, nhưng AI là động cơ:** Để động cơ chạy tốt, dữ liệu đầu vào (cho RAG hoặc Training) phải sạch và được tổ chức tốt.
  - **Đừng phát minh lại cái bánh xe:** Tận dụng các dịch vụ Managed Services như Bedrock hay SageMaker giúp đi nhanh hơn rất nhiều so với việc tự xây dựng hạ tầng từ đầu.
  - **AI không thay thế con người, nhưng người biết dùng AI sẽ thay thế người không biết:** Việc thành thạo các công cụ như Bedrock là một lợi thế cạnh tranh cực lớn trên thị trường tuyển dụng hiện nay.
