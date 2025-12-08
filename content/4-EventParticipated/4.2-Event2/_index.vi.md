---
title: "Event 2"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

### AI-Driven Development Workshop – Shaping the Future of Development

**Diễn giả chính:** Anh Toan Huynh & Chị My Nguyen

**Đội ngũ điều phối:** Diem My, Dai Truong, Dinh Nguyen

### Mục tiêu chuyên môn
Sự kiện tập trung vào việc định hình lại tư duy lập trình trong kỷ nguyên mới, với các mục tiêu cốt lõi:
- **Cập nhật xu hướng công nghệ:** Phân tích sự chuyển dịch từ lập trình thủ công sang mô hình Phát triển do AI điều phối (AI-Driven Development - AI-DD).
- **Giới thiệu Framework:** Ra mắt mô hình vòng đời phát triển AI-DLC, đặt nền móng cho việc tích hợp trí tuệ nhân tạo vào từng điểm chạm của quy trình CI/CD.
- **Thực nghiệm công cụ:** Demo chuyên sâu khả năng của Amazon Q Developer và Kiro IDE Extension trong môi trường production.
- **Tối ưu hóa quy trình:** Minh chứng cách AI giải quyết bài toán cân bằng giữa Tốc độ (Velocity), Chất lượng (Quality) và Năng suất (Productivity).
- **Định hướng nghề nghiệp:** Xác định lại vị thế và kỹ năng cần thiết của kỹ sư phần mềm khi AI trở thành cộng sự cốt cán.

### Nội dung chi tiết và Điểm nhấn kỹ thuật

#### 1. Tầm nhìn: Shaping the Future of Development
Mở đầu hội thảo, diễn giả Toan Huynh đã khắc họa bức tranh toàn cảnh về kỷ nguyên **AI-Orchestrated Development**. Đây không đơn thuần là việc sử dụng công cụ hỗ trợ, mà là sự thay đổi hệ hình (paradigm shift), nơi AI chuyển từ vai trò "thợ phụ" sang vị trí trung tâm trong việc điều phối luồng công việc, từ khâu lên ý tưởng, thiết kế kiến trúc cho đến deployment.

#### 2. Phân tích thực trạng và Sự ra đời của AI-Driven Development (AI-DD)
Bài tham luận chỉ ra điểm nghẽn của các mô hình hiện tại (AI-Assisted/AI-Managed): sự thiếu ổn định trong output và khó khăn trong việc kiểm soát context (ngữ cảnh).
Giải pháp được đưa ra là **AI-Driven Development (AI-DD)**. Đây là điểm cân bằng tối ưu, nơi tự động hóa được đẩy lên cao nhưng vẫn duy trì cơ chế "Human-in-the-loop" (con người trong vòng lặp) để đảm bảo tính chính xác và trách nhiệm giải trình.

#### 3. Mô hình vòng đời phát triển AI (AI-DLC)
Điểm nhấn lý thuyết quan trọng nhất là mô hình phân cấp sự tiến hóa của AI trong SDLC:
- **Level 1 - AI-Assisted Development:** AI đóng vai trò như một "Smart Linter", hỗ trợ gợi ý code (autocomplete), refactor cơ bản và check cú pháp.
- **Level 2 - AI-Driven Development (Trọng tâm):** AI tham gia sâu vào tầng chiến lược như thiết kế High-level Design, hoạch định tasks và hỗ trợ ra quyết định logic.
- **Level 3 - AI-Managed Development:** Hướng tới các AI Agents tự hành, tự động thực thi quy trình phát triển dưới sự giám sát và phê duyệt cuối cùng của con người.
Trong mô hình AI-DD, AI được ví như một "Technical Lead" ảo, còn Developer đóng vai trò người đánh giá và ra quyết định (Reviewer & Decision Maker).

#### 4. Bảy trụ cột lợi ích (The 7 Pillars of AI Benefits)
Việc áp dụng AI-DD mang lại tác động đa chiều, được tóm gọn qua 7 từ khóa:
* **Predictability:** Dự báo rủi ro và tiến độ chính xác hơn.
* **Velocity:** Tăng tốc độ đưa sản phẩm ra thị trường (Time-to-market).
* **Quality:** Giảm thiểu lỗi logic và bảo mật.
* **Innovation:** Giải phóng nhân sự khỏi các tác vụ lặp lại để tập trung sáng tạo.
* **Developer Engagement:** Giảm burnout, tăng hứng thú công việc.
* **Customer Satisfaction:** Phản hồi nhanh với nhu cầu khách hàng.
* **Productivity:** Tối ưu hóa hiệu suất tổng thể.

#### 5. Tác động lên quy trình SDLC
AI đang tái cấu trúc chuỗi giá trị phần mềm: *Explore & Plan → Create → Test & Secure → Review & Deploy → Maintain*. Đặc biệt, các nút thắt cổ chai truyền thống như viết Unit Test, Documentation, và Security Scanning được AI xử lý với tốc độ vượt trội, giúp quy trình mượt mà hơn (frictionless).

#### 6. Live Demo: Sức mạnh của Amazon Q và Kiro IDE
Phiên demo thực tế đã chứng minh lý thuyết qua hai công cụ mạnh mẽ:

**Amazon Q Developer (Trợ lý chuyên biệt cho AWS):**
- Tích hợp sâu vào IDE (VS Code, Cloud9), hoạt động như một chuyên gia AWS ngay bên cạnh.
- Khả năng hiểu ngữ cảnh dự án để sinh code, tự động tạo Unit Test và viết tài liệu kỹ thuật.
- Điểm ấn tượng: Hỗ trợ cập nhật `prompt.md` để tinh chỉnh ngữ cảnh và tự động hóa các pipeline CI/CD phức tạp.

**Kiro IDE Extension (Trình bày bởi chị My Nguyen):**
- Minh họa triết lý "Documentation as Code".
- Quản lý dự án thông qua các file markdown đặc tả (`requirements.md`, `design.md`, `tasks.md`).
- **Use-case:** Xây dựng ứng dụng Chat có tính năng Authentication. Chỉ từ các mô tả ngôn ngữ tự nhiên, AI đã thiết kế luồng API, sinh code backend và cấu trúc database một cách mạch lạc.

### Trải nghiệm và Góc nhìn cá nhân
Tham dự workshop này là một bước ngoặt trong tư duy nghề nghiệp của tôi. Thay vì chỉ tập trung vào việc viết đúng cú pháp (syntax) như trước đây, tôi nhận ra trọng tâm công việc đang dịch chuyển.
- **Sự kinh ngạc về công nghệ:** Chứng kiến Amazon Q và Kiro IDE dựng lên bộ khung dự án hoàn chỉnh từ vài dòng prompt khiến tôi thực sự ấn tượng (wow factor). Nó cho thấy khoảng cách từ ý tưởng đến sản phẩm đang được rút ngắn chưa từng thấy.
- **Giải tỏa tâm lý:** Những chia sẻ từ anh Toan Huynh đã giúp tôi gạt bỏ nỗi lo "AI thay thế lập trình viên". Thay vào đó, tôi nhìn thấy cơ hội để trở thành một "Super Developer" khi biết tận dụng đòn bẩy công nghệ.
- **Ứng dụng ngay:** Tôi đã bắt đầu tích hợp Amazon Q vào quy trình debug hàng ngày và nhận thấy hiệu suất cải thiện rõ rệt, đặc biệt là trong việc giải thích các lỗi logic phức tạp.

### Bài học và Định hướng hành động
Từ những kiến thức thu được, tôi rút ra ba bài học cốt tử cho lộ trình phát triển bản thân:
1.  **Chuyển đổi vị thế - AI là Cộng sự:** Ngừng cạnh tranh với máy móc, thay vào đó tập trung rèn luyện kỹ năng **Prompt Engineering** và giao tiếp ngữ cảnh để tối ưu hóa đầu ra của AI.
2.  **Tư duy Kiến trúc (Architectural Mindset) là vua:** Khi việc viết code (Implementation) trở nên dễ dàng nhờ AI, giá trị cốt lõi của kỹ sư phần mềm sẽ nằm ở khả năng Thiết kế hệ thống (System Design), Tư duy phản biện và Kiểm soát chất lượng (Quality Assurance).
3.  **Thích ứng linh hoạt (Agility):** Mô hình AI-DLC không phải là tương lai xa mà là tiêu chuẩn hiện tại. Việc thành thạo các công cụ AI-native ngay bây giờ là chìa khóa để tạo lợi thế cạnh tranh trong thị trường lao động.