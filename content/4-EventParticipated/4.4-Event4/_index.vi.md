---
title: "Event 4"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

### AWS Cloud Mastery Series #2: Workshop DevOps trên AWS

### Mục Đích Của Sự Kiện

Buổi workshop được thiết kế nhằm mục tiêu thu hẹp khoảng cách giữa lý thuyết DevOps và việc triển khai thực tế trên môi trường Cloud. Không chỉ dừng lại ở việc giới thiệu công cụ, sự kiện tập trung vào việc xây dựng tư duy hệ thống, giúp người tham dự nắm bắt được luồng công việc (workflow) chuẩn từ khâu phát triển (Development) sang vận hành (Operations). Trọng tâm là làm chủ các dịch vụ cốt lõi của AWS để xây dựng quy trình CI/CD, quản lý hạ tầng dưới dạng mã (IaC), vận hành container và thiết lập hệ thống giám sát (Observability) hiệu quả.

### Tổng Quan Chương Trình

Chương trình cung cấp một cái nhìn toàn cảnh về lộ trình phát triển năng lực trên AWS:

  - **Định hướng lộ trình chứng chỉ:** Phân tích lộ trình thăng tiến kỹ năng thông qua các chứng chỉ như *AWS Certified Solutions Architect* (kiến trúc), *SysOps Administrator* (vận hành) và đích đến cao hơn là *AWS Certified DevOps Engineer – Professional*.
  - **Tài nguyên mở rộng:** Cung cấp hệ sinh thái các bài lab thực hành (hands-on labs), tài liệu whitepapers và cộng đồng hỗ trợ để học viên duy trì việc học sau sự kiện.

### Nội Dung Nổi Bật

Dưới sự hướng dẫn của các chuyên gia AWS, workshop đi sâu vào các khía cạnh kỹ thuật then chốt:

  - **CI/CD Pipeline toàn diện:** Khám phá cách **AWS CodePipeline** đóng vai trò như "xương sống" để tự động hóa quy trình release phần mềm. Tích hợp từ khâu source code (CodeCommit/GitHub), build (CodeBuild) đến deploy (CodeDeploy), đảm bảo tính nhất quán giữa các môi trường.
  - **Infrastructure as Code (IaC):** So sánh và ứng dụng hai phương pháp tiếp cận: **AWS CloudFormation** (định nghĩa hạ tầng qua JSON/YAML) và **AWS CDK** (Cloud Development Kit - cho phép dùng ngôn ngữ lập trình quen thuộc như TS/Python để dựng hạ tầng). CDK đặc biệt gây ấn tượng nhờ khả năng tối ưu trải nghiệm cho developer.
  - **Hệ sinh thái Container:** Phân tích các lựa chọn dựa trên bài toán thực tế: **Amazon ECS** cho sự đơn giản, tích hợp sâu với AWS; **Amazon EKS** cho các hệ thống phức tạp dùng Kubernetes; và **AWS App Runner** cho các ứng dụng web cần triển khai nhanh chóng mà không lo về quản lý hạ tầng.
  - **Observability (Khả năng quan sát):** Đi xa hơn việc "monitoring" cơ bản. Kết hợp **Amazon CloudWatch** (thu thập logs, metrics) và **AWS X-Ray** (distributed tracing) để có cái nhìn sâu sắc vào sức khỏe ứng dụng và trải nghiệm người dùng cuối.
  - **Văn Hóa & Best Practices:** Nhấn mạnh rằng công cụ chỉ là phương tiện. Thành công đến từ việc áp dụng *Feature Flags* để giảm rủi ro khi deploy, chiến lược *Automated Testing* chặt chẽ và quy trình xử lý sự cố (Incident Management) minh bạch.

### Những Gì Tôi Học Được

  - **Tư duy "Culture First":** Tôi nhận ra rào cản lớn nhất của DevOps không phải là công nghệ mà là sự kháng cự thay đổi. Một team DevOps thành công cần sự cộng tác chặt chẽ (collaboration) và chia sẻ trách nhiệm.
  - **Sức mạnh của Tự động hóa:** Tự động hóa pipeline không chỉ giúp tăng tốc độ release (velocity) mà còn đảm bảo tính ổn định (reliability), loại bỏ các lỗi sai sót do thao tác thủ công của con người.
  - **IaC là "Version Control" cho Hạ tầng:** Việc coi hạ tầng như source code giúp team có thể review, audit và roll-back (khôi phục) môi trường nhanh chóng khi có sự cố, giải quyết triệt để vấn đề "configuration drift" (sai lệch cấu hình).
  - **Chiến lược chọn Container:** Không có giải pháp "one-size-fits-all". Việc lựa chọn giữa ECS hay EKS phụ thuộc rất lớn vào quy mô đội ngũ vận hành và yêu cầu cụ thể của dự án.
  - **Tầm quan trọng của Tracing:** Trong kiến trúc microservices, nếu thiếu distributed tracing (như X-Ray), việc tìm nguyên nhân gốc rễ (root cause analysis) khi hệ thống chậm giống như mò kim đáy bể.

### Ứng Dụng Vào Công Việc

Từ những kiến thức đã thu nạp, tôi dự định áp dụng vào dự án thực tập hiện tại:

  - **Thiết lập CI/CD Pipeline:** Đề xuất chuyển đổi quy trình deploy thủ công hiện tại sang sử dụng AWS CodePipeline để tự động hóa việc đẩy code lên môi trường Staging.
  - **Triển khai IaC:** Bắt đầu viết các script CloudFormation hoặc CDK đơn giản để dựng môi trường, thay vì thao tác click trên Console (ClickOps), giúp việc bàn giao dự án sau này dễ dàng hơn.
  - **Đánh giá Container hóa:** Nghiên cứu dockerize một số module nhỏ của dự án và thử nghiệm deploy trên AWS App Runner để đánh giá hiệu năng.
  - **Tối ưu hóa Monitoring:** Cấu hình thêm các CloudWatch Alarms để cảnh báo ngay lập tức qua SNS/Email khi CPU hoặc Memory vượt ngưỡng cho phép, thay vì đợi hệ thống "sập" mới biết.

### Trải Nghiệm Cá Nhân & Bài Học Rút Ra

Trước khi tham gia workshop, khái niệm DevOps đối với tôi khá mơ hồ, thường bị nhầm lẫn là chỉ việc sử dụng Docker hay Jenkins. Tuy nhiên, buổi workshop này đã thực sự thay đổi tư duy của tôi:

**1. Cảm giác làm chủ quy trình:**
Khoảnh khắc nhìn thấy dòng chữ "Succeeded" màu xanh trên CodePipeline chạy tự động từ lúc commit code cho đến khi ứng dụng được cập nhật trên môi trường production mang lại cảm giác cực kỳ thỏa mãn. Nó giúp tôi hiểu rằng, nhiệm vụ của Developer không chỉ là viết code, mà là đảm bảo code đó chạy tốt trên môi trường thực tế.

**2. X-Ray:**
Phần thực hành về Observability với AWS X-Ray là điểm nhấn ấn tượng nhất. Nó giống như việc bác sĩ chụp X-quang cho ứng dụng vậy; tôi có thể nhìn thấy chính xác request đang bị tắc nghẽn ở database hay API nào. Điều này giúp loại bỏ sự đoán mò khi debug.

**3. Bài học:**

  - **Tự động hóa là bắt buộc:** Nguyên tắc "Nếu phải làm thủ công quá 2 lần, hãy tự động hóa nó" sẽ là kim chỉ nam cho tôi.
  - **DevOps là trách nhiệm chung (Shared Responsibility):** Hiểu về quy trình vận hành giúp tôi viết code "thân thiện" hơn với hệ thống (cloud-native), dễ deploy và dễ scale hơn.
  - **Đo lường mọi thứ:** Không thể cải thiện những gì mình không đo lường được. Metrics và Logs phải được coi trọng ngang hàng với tính năng của sản phẩm ngay từ ngày đầu tiên (Day 1).
