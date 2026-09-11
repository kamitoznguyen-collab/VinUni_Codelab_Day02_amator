# 📝 Nhật Ký Tương Tác AI & Bài Học Phản Ánh (AI Log & Reflection)
## Đơn vị: Vin Smart Future — Dự Án VinUni Smart Canteen Co-pilot

---

## 🤖 1. Tổng Quan Quá Trình Sử Dụng AI Làm Cộng Sự (Thought-Partner)

Trong suốt quá trình thực hiện **Lab 02: AI Product Scoping**, nhóm kỹ sư Vin Smart Future đã sử dụng mô hình ngôn ngữ lớn (**Google Gemini 2.5 Flash / Claude**) như một người phản biện kỹ thuật, đóng vai trò đồng thời là:
1. **Trưởng phòng Vận hành Canteen (Operations Director):** Để tìm ra các điểm nghẽn thực tế và con số thời gian lãng phí.
2. **Kỹ sư Trưởng AI (Principal AI Architect):** Để phản biện xem bài toán có thực sự cần AI hay chỉ cần code Rule-based thông thường.

---

## 💡 2. AI Đã Giúp Gì Cho Nhóm? (What AI Did Well)

* **Brainstorming bài toán thực tế theo 4 Lenses:** Khi ban đầu nhóm chỉ nghĩ đến các bài toán chung chung của VinFast hay Xanh SM, AI đã hỗ trợ đào sâu vào hệ sinh thái giáo dục **VinUni**, chỉ ra điểm nghẽn nhức nhối về quy trình mua vé 2 chặng tại Canteen trong khung giờ cao điểm trưa (11h45 - 12h30).
* **Định lượng hoá Success Metrics:** AI đã giúp nhóm chuyển đổi các mục tiêu mơ hồ (như *"làm canteen nhanh hơn"*) thành các con số kỹ thuật có thể đo lường và kiểm chứng:
  * Rút ngắn thời gian chờ từ **18 phút xuống dưới 3 phút/lượt**.
  * Cắt giảm lượng thức ăn dư thừa cuối ngày từ **18% xuống dưới 5%**.
* **Xây dựng cấu trúc Operational Boundaries (Ranh giới an toàn):** AI giúp nhóm hình dung các tình huống rủi ro mà một hệ thống tự động có thể gặp phải (như tự trừ tiền tài khoản sinh viên hoặc đưa ra cảnh báo sai lệch về an toàn dinh dưỡng).

---

## ⚠️ 3. AI Đã Trả Lời Sai / Ảo Giác (Hallucination) Ở Đâu?

Trong các lượt prompt đầu tiên, AI đã mắc một số sai lầm nghiêm trọng về tư duy thiết kế sản phẩm:
1. **Lạm dụng công nghệ quá đà (Over-engineering):**
   * *Sai sót của AI:* AI ban đầu đề xuất xây dựng một hệ thống **Autonomous Multi-Agent Swarm** kết hợp cánh tay robot tự động chia cơm và phân loại thức ăn bằng Computer Vision 3D.
   * *Thực tế:* Giải pháp này cực kỳ đắt đỏ, không khả thi về mặt chi phí và rủi ro hỏng hóc cao trong môi trường canteen dầu mỡ.
2. **Ảo giác về quy chế thanh toán:**
   * *Sai sót của AI:* AI đề xuất tự động quét nhận diện khuôn mặt sinh viên đi qua cửa và tự động trừ tiền ví điện tử ngay lập tức mà không cần xác nhận.
   * *Hậu quả:* Đây là vi phạm nghiêm trọng về an toàn tài chính và quyền riêng tư sinh viên nếu nhận diện nhầm người.

---

## 🛠️ 4. Nhóm Đã Tinh Chỉnh Prompt & Đặt Ranh Giới An Toàn Thế Nào?

Để khắc phục các điểm yếu trên, nhóm đã thực hiện các bước điều chỉnh:
* **Thu hẹp Scope (Problem First, AI Second):** Yêu cầu AI đóng vai trò một CFO khó tính để cắt giảm giải pháp xuống mức tối giản nhất: **Rule-based cho thanh toán + LLM Feature cho việc gợi ý món ăn dinh dưỡng & dự báo số lượng suất cho bếp trưởng**.
* **Thiết lập ranh giới bắt buộc có người duyệt (Human-in-the-loop - HITL):**
  * Buộc mọi lệnh dự báo suất ăn phải có tiền tố `[DRAFT_ONLY]` để Bếp trưởng kiểm tra và phê duyệt số lượng trước khi nấu.
  * Sinh viên luôn phải chủ động bấm xác nhận thanh toán hoặc quét mã bảo mật trước khi tiền bị trừ.
* **Cơ chế Fallback rõ ràng:** Thiết lập quy trình dự phòng: nếu hệ thống AI hay đường truyền gặp sự cố, canteen chuyển đổi ngay sang quầy POS quẹt thẻ sinh viên truyền thống trong vòng 10 giây.

---

## 🎓 5. Bài Học Cá Nhân (Key Takeaways)
* *"AI không thay thế tư duy phản biện của kỹ sư sản phẩm."* AI đưa ra ý tưởng rất nhanh nhưng có xu hướng phóng đại độ phức tạp (Over-hyping AI).
* Thành công của một dự án AI tại Vingroup không nằm ở việc dùng mô hình to bao nhiêu, mà nằm ở việc **vẽ ranh giới an toàn (Operational Boundary) đủ chặt chẽ** để hệ thống vận hành trơn tru và an toàn trong thực tế.
