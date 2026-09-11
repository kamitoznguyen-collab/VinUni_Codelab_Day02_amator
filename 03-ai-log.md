# 📝 Phase 6 — REFLECTION: Nhật Ký Tương Tác AI & Bài Học Cá Nhân (Duy)
## Đơn vị: Vin Smart Future — Dự Án VinUni Smart Canteen App

---

## 🤖 1. Bối Cảnh: Sử Dụng AI Làm Cộng Sự Tư Duy (Thought-Partner)

Trong suốt buổi làm việc **Lab 02: AI Product Scoping**, tôi (**Duy**) đã trực tiếp làm việc cùng các mô hình ngôn ngữ lớn (LLM) để đóng vai trò đồng phản biện (devil's advocate) trong việc tìm kiếm và scoping bài toán vận hành tại Canteen Đại học VinUni.

---

## 💡 2. AI Đã Hỗ Trợ Tôi Như Thế Nào? (What AI Did Well)

1. **Bóc tách điểm nghẽn thực tế (Root Cause Analysis):** 
   * Ban đầu tôi chỉ nhận thấy hiện tượng bề mặt là "sinh viên xếp hàng mua vé quá lâu". Khi thảo luận và yêu cầu AI phân tích luồng di chuyển, AI đã cùng tôi bóc tách ra điểm nghẽn cốt lõi nhất: Việc **vé ăn giấy hoàn toàn không ghi món** buộc sinh viên phải đứng phân vân chọn từng món mặn/rau/canh trực tiếp tại khay, làm tê liệt toàn bộ hàng đợi phía sau.
2. **Định lượng hoá Success Metrics:**
   * AI hỗ trợ tôi chuyển đổi mong muốn cải thiện chung chung thành các con số kỹ thuật cụ thể:
     * Rút ngắn thời gian chờ nhận cơm từ **18 phút ──► dưới 3 phút/người** (tiết kiệm 83% thời gian).
     * Tăng năng lực phục vụ giờ cao điểm từ 120 suất/giờ ──► **400 suất/giờ**.
     * Cắt giảm thức ăn dư thừa của nhà bếp từ 18% ──► **dưới 5%**.
3. **Định hình tính năng Ứng dụng Di Động:**
   * AI gợi ý ý tưởng xây dựng tính năng **AI gợi ý món ăn theo thói quen (Habit-based Recommender)** kết hợp **Đặt món trước (Pre-ordering) và Mua vé thanh toán trực tuyến**, giúp giải quyết triệt để quy trình mua vé 2 chặng thủ công.

---

## ⚠️ 3. AI Đã Trả Lời Sai / Ảo Giác (Hallucination) Ở Đâu?

1. **Ảo giác về độ phức tạp (Over-engineering):**
   * Trong những lượt prompt đầu tiên, AI đã vẽ ra một giải pháp quá đao to búa lớn: lắp đặt hệ thống cánh tay robot tự động chia thức ăn bằng Computer Vision 3D tại canteen. Đây là giải pháp cực kỳ đắt đỏ, dễ hỏng hóc và hoàn toàn phi thực tế đối với một canteen trường đại học.
2. **Vi phạm ranh giới an toàn tài chính (Safety Boundary Breach):**
   * AI từng gợi ý tính năng "tự động nhận diện khuôn mặt sinh viên đi qua cửa canteen và tự động trừ tiền trong ví điện tử". Tôi đã nhận diện ngay đây là một rủi ro bảo mật nghiêm trọng có thể dẫn đến trừ tiền nhầm nếu nhận diện sai hoặc sinh viên chỉ ghé vào canteen mua chai nước.

---

## 🛠️ 4. Tôi Đã Tinh Chỉnh Prompt & Đặt Ranh Giới An Toàn (Operational Boundary) Ra Sao?

1. **Kéo AI về bài toán thực tế (Problem First, AI Second):**
   * Tôi yêu cầu AI đóng vai trò một Giám đốc Tài chính (CFO) khắt khe, cắt giảm giải pháp xuống kiến trúc tối giản: Rule-based cho thanh toán an toàn, và LLM Feature cho việc cá nhân hóa thực đơn theo thói quen sinh viên.
2. **Bắt buộc cơ chế Human-in-the-loop (HITL):**
   * Tôi đặt ranh giới nghiêm ngặt: Mọi gợi ý món ăn và hóa đơn tạm tính phải có nhãn `[DRAFT_ONLY]`. Sinh viên BẮT BUỘC phải là người chủ động nhấn xác nhận thanh toán thì tiền mới được trừ và tạo mã QR E-Ticket.
3. **Cơ chế Fallback an toàn:**
   * Luôn duy trì 1 quầy quẹt thẻ sinh viên POS truyền thống đề phòng trường hợp mất mạng hoặc sinh viên hết pin điện thoại.

---

## 🎓 5. Bài Học Cá Nhân Tâm Đắc Nhất
> *"AI là một trợ lý brainstorm ý tưởng xuất sắc và đa chiều, nhưng kỹ sư AI Product phải là người nắm giữ tay lái, thiết lập ranh giới an toàn (Operational Boundary) và kiểm định tính khả thi trong thực tế."*
