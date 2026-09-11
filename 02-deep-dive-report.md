# 📄 Bài Nộp Cá Nhân — Lab 02: AI Product Scoping (Vin Smart Future)
## Sinh viên thực hiện: Duy — Nhóm Kỹ sư AI Product Vin Smart Future
### Đơn vị nghiên cứu: Đại học VinUni (Campus Life & Canteen Operations)

---

## 🏛️ Bối cảnh cá nhân: Tôi là ai?

Tôi là **Duy**, Kỹ sư AI Product tại **Vin Smart Future** (Tập đoàn Vingroup), phụ trách mảng nghiên cứu và ứng dụng giải pháp trí tuệ nhân tạo nâng cao trải nghiệm sinh viên tại khuôn viên Đại học VinUni (Vinhomes Ocean Park).

Qua khảo sát thực tế đời sống sinh viên và vận hành tại Canteen trung tâm VinUni vào các khung giờ cao điểm trưa (11h45 – 12h30), tôi nhận thấy sinh viên và giảng viên đang phải đối mặt với sự lãng phí thời gian rất lớn do quy trình mua vé 2 chặng: **Thanh toán nhận vé giấy chung (hoàn toàn không ghi món) ──► Cầm vé sang quầy thức ăn xếp hàng lượt 2 ──► Đến lượt mới đứng ngắm khay và chọn đồ ăn trực tiếp**. 

Báo cáo cá nhân này ghi nhận toàn bộ quá trình tôi thực hiện **Phase 1 (SCAN)**, **Phase 2 (QUICK-ASSESS)** và **Phase 6 (REFLECTION)** trong buổi Lab 02 hôm nay.

---

# 🔍 Phase 1 — SCAN: Tìm Kiếm Cơ Hội Qua 4 Lenses (Cá nhân)

Sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác) để quét qua các hoạt động vận hành tại VinUni và hệ sinh thái Vingroup:

| # | Đơn vị thành viên | Lens áp dụng | Mô tả ngắn bài toán & Điểm nghẽn vận hành |
|---|-------------------|--------------|-------------------------------------------|
| 1 | **VinUni** (Canteen) | **Lặp lại & Tốn thời gian** | Quy trình mua vé 2 chặng: Thanh toán mua vé giấy chung (hoàn toàn KHÔNG ghi món) ──► Cầm vé sang quầy thức ăn xếp hàng lượt 2 ──► Đến lượt mới đứng ngắm khay và chọn đồ ăn trực tiếp. Sinh viên phân vân chọn món làm nghẽn quầy (18-20 phút/lượt), nhà bếp "nấu mù" không dự báo được số lượng suất từng món. |
| 2 | **VinUni** (Thư viện) | **Pain từ người khác** | Tranh chấp và lãng phí phòng học nhóm (Discussion Pods): Tỷ lệ đặt chỗ ảo ("bỏ bom" no-show) lên tới 35%, sinh viên cần phòng thì hệ thống báo hết, thủ thư mất 15-20 phút/lần đi kiểm tra thực địa và can thiệp giải quyết. |
| 3 | **VinUni** (Phòng Đào tạo) | **Lặp lại & AI-upgrade** | Nhân viên Registrar quá tải hàng trăm email/ticket xin đổi lịch thi, rút môn Add/Drop, xin cấp giấy chứng nhận sinh viên đầu kỳ. Mất 12 phút/email tra cứu quy chế lặp đi lặp lại, sinh viên chờ 3-5 ngày mới nhận phản hồi. |
| 4 | **Xanh SM** (GSM) | **Tốn thời gian** | Điều phối viên xử lý thủ công các phản hồi khẩn cấp từ tài xế taxi điện khi pin báo dưới 5% hoặc tìm trạm sạc VinFast còn trụ trống, mất 15 phút tra cứu thủ công toạ độ và tình trạng trụ. |
| 5 | **VinFast** (EV Service) | **AI-upgrade** | Khách hàng mô tả lỗi xe điện bằng tiếng Việt đời thường (ví dụ: *"đi qua gờ giảm tốc bánh trước kêu lục cục"*), nhân viên tiếp nhận mất nhiều thời gian hỏi đi hỏi lại trước khi phân loại đúng mã lỗi kỹ thuật vào xưởng. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ Bài Toán Tiềm Năng (Cá nhân)

---

### 📌 Thẻ 1: VinUni Canteen — Ứng dụng đặt món trước & Gợi ý AI theo thói quen
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Mua vé giấy chung (không ghi món) rồi mới ra quầy │
│ đứng chọn đồ ăn trực tiếp, gây ùn ứ kép tại Canteen VinUni. │
│ Đơn vị thành viên: [x] VinUni (Dịch vụ Đời sống & Canteen)  │
│                                                             │
│ Ai đang đau? Sinh viên/Giảng viên (mất 20 min chờ),          │
│ Thu ngân (quá tải thanh toán), Nhà bếp (lãng phí 18% đồ ăn)  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Xếp hàng quầy thu ngân -> 2. Thanh toán nhận vé chung  │
│   (VÉ KHÔNG GHI MÓN) -> 3. Xếp hàng quầy thức ăn            │
│   -> 4. Đứng chọn đồ ăn trực tiếp tại khay -> 5. Xé vé lấy đĩa│
│                                                             │
│ Bước nào tốn thời gian nhất? Bước 1, 3, 4 (⏱ 16-18 phút)   │
│ AI có thể hỗ trợ ở bước nào? Bước 1-2 (Gợi ý món theo thói  │
│ quen, đặt trước & thanh toán trên App) & Bước 3 (Bếp KDS)   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian chờ nhận cơm từ 18 phút ──> dưới 3 phút/lượt. │
│ Tỷ lệ thức ăn dư thừa giảm từ 18% ──> dưới 5%.              │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Mobile E-Payment App  │
└─────────────────────────────────────────────────────────────┘
```

---

### 📌 Thẻ 2: VinUni Thư Viện — Điều phối phòng thảo luận nhóm & xử lý No-show
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Sinh viên đặt phòng học nhóm trước nhưng không đến│
│ (no-show 35%), gây lãng phí phòng và tạo tranh chấp chỗ.    │
│ Đơn vị thành viên: [x] VinUni (Dịch vụ Thư viện)            │
│                                                             │
│ Ai đang đau? Sinh viên cần phòng học (bị báo ảo hết phòng), │
│ Thủ thư (mất 20 phút đi giải quyết tranh chấp phòng trực tiếp)│
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Đặt phòng online -> 2. Đến nhận phòng (phát hiện lấn)   │
│   -> 3. Đi gọi thủ thư can thiệp -> 4. Thủ thư tra cứu & mời ra│
│                                                             │
│ Bước nào tốn thời gian nhất? Bước 3-4 (⏱ 15 phút xử lý)     │
│ AI có thể hỗ trợ ở bước nào? Bước 2-3 (Tự động quét phòng   │
│ trống sau 10 min no-show & re-allocate ngay trên app)       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Tăng tỷ lệ sử dụng hiệu dụng phòng thảo luận từ 55% ──> 92%. │
│ Thời gian giải quyết tranh chấp giảm từ 15 min ──> 1 min.    │
│                                                             │
│ Quick Architecture: [x] IoT Rule Engine + Smart Scheduler    │
└─────────────────────────────────────────────────────────────┘
```

---

### 📌 Thẻ 3: VinUni Phòng Đào Tạo — Trợ lý giải đáp học vụ & thủ tục sinh viên
```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Hàng trăm email hỏi đáp quy chế đào tạo, đổi môn  │
│ Add/Drop đầu kỳ bị nghẽn, sinh viên chờ 3-5 ngày phản hồi.  │
│ Đơn vị thành viên: [x] VinUni (Phòng Quản lý Đào tạo)       │
│                                                             │
│ Ai đang đau? Cán bộ đào tạo (gõ trả lời lặp lại),           │
│ Sinh viên (lo lắng vì trễ deadline đăng ký học phần)        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhận email sinh viên -> 2. Tra cứu sổ tay quy chế      │
│   -> 3. Mở phần mềm tra cứu điểm/tín chỉ -> 4. Viết email rep│
│                                                             │
│ Bước nào tốn thời gian nhất? Bước 2-4 (⏱ 12 phút/email)     │
│ AI có thể hỗ trợ ở bước nào? Bước 2-4 (RAG tra cứu quy chế, │
│ draft sẵn câu trả lời có tag [DRAFT_ONLY] cho cán bộ duyệt) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Rút ngắn thời gian phản hồi email từ 72 giờ ──> dưới 2 giờ. │
│ Giảm 80% thời gian soạn thảo thủ công của cán bộ đào tạo.   │
│                                                             │
│ Quick Architecture: [x] LLM Feature (RAG + Co-pilot HITL)   │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Đề xuất cá nhân gửi lên Nhóm:
Tôi đề xuất nhóm lựa chọn **Thẻ #1 (VinUni Canteen)** để làm bài toán chung cho nhóm vì tính cấp thiết cao nhất, chạm đến 100% sinh viên hàng ngày và có dữ liệu lịch học Canvas sẵn sàng tích hợp.

*(Phần phân tích chi tiết quy trình tương lai Phase 3, lập trình mẫu Phase 4 và đánh giá khả thi Phase 5 sẽ do cả nhóm thống nhất thực hiện trên nhánh main).*

---

# 📝 Phase 6 — REFLECTION: Nhật Ký Tương Tác AI & Bài Học Cá Nhân (Duy)

### 1. AI đã hỗ trợ tôi những gì trong vai trò Cộng sự tư duy (Thought-Partner)?
* **Bóc tách điểm nghẽn thực tế:** Khi bắt đầu, tôi chỉ nghĩ đến việc "xếp hàng mua vé bị chậm". Khi trao đổi cùng AI, AI đã giúp tôi nhìn sâu vào nguyên nhân cốt lõi: Việc **vé ăn không in tên món** là nút thắt chí mạng khiến sinh viên khi đến lượt tại quầy thức ăn mới bắt đầu ngắm nghía, hỏi món và chọn đồ, gây ùn ứ tê liệt toàn bộ hàng dài phía sau.
* **Định lượng hóa mục tiêu sản phẩm:** AI giúp tôi chuyển đổi mong muốn cải thiện chung chung thành các chỉ số kỹ thuật có thể đo lường:
  * Rút ngắn thời gian chờ nhận cơm từ **18 phút xuống dưới 3 phút/lượt**.
  * Giảm lãng phí thực phẩm dư thừa của nhà bếp từ **18% xuống dưới 5%**.
* **Định hình giải pháp sản phẩm:** Cùng tôi phác thảo giải pháp ứng dụng di động **VinUni Smart Canteen App** kết hợp tính năng **AI gợi ý món ăn theo thói quen & dinh dưỡng** giúp sinh viên đặt trước món ăn và thanh toán vé điện tử E-Ticket ngay trên lớp học.

### 2. AI đã trả lời sai / ảo giác (Hallucination) ở đâu?
* **Ảo giác về giải pháp (Over-engineering):** Trong những lượt prompt đầu tiên, AI đã đề xuất một mô hình quá đao to búa lớn: lắp đặt hệ thống cánh tay robot tự động chia cơm bằng Computer Vision 3D tại canteen. Đây là giải pháp cực kỳ đắt đỏ, dễ hỏng hóc và hoàn toàn không thực tế với môi trường trường đại học.
* **Vi phạm ranh giới an toàn tài chính:** AI từng gợi ý tính năng "tự động nhận diện khuôn mặt sinh viên đi qua cửa và tự động trừ tiền trong ví điện tử". Tôi đã nhận diện ngay đây là rủi ro bảo mật nghiêm trọng có thể dẫn đến trừ tiền nhầm nếu nhận diện sai hoặc sinh viên chỉ đi ngang qua canteen.

### 3. Tôi đã tinh chỉnh Prompt & Thiết lập ranh giới an toàn (Operational Boundary) như thế nào?
* **Kéo AI về bài toán thực tế (Problem First, AI Second):** Tôi yêu cầu AI đóng vai trò một Giám đốc Tài chính khắt khe, cắt giảm giải pháp xuống kiến trúc tối giản: Rule-based cho thanh toán an toàn, và LLM Feature cho việc cá nhân hóa thực đơn theo thói quen sinh viên.
* **Bắt buộc cơ chế Human-in-the-loop (HITL):** Tôi đặt ranh giới nghiêm ngặt rằng mọi gợi ý món ăn và hóa đơn tạm tính phải có nhãn `[DRAFT_ONLY]`. Sinh viên BẮT BUỘC phải là người chủ động nhấn xác nhận thanh toán thì tiền mới được trừ.
* **Cơ chế Fallback an toàn:** Luôn duy trì 1 quầy quẹt thẻ sinh viên POS truyền thống đề phòng trường hợp mất mạng hoặc sinh viên hết pin điện thoại.

### 4. Bài học tâm đắc nhất của tôi sau bài Lab:
> *"AI là một trợ lý brainstorm ý tưởng xuất sắc và đa chiều, nhưng kỹ sư AI Product phải là người nắm giữ tay lái, thiết lập ranh giới an toàn (Operational Boundary) và kiểm định tính khả thi trong thực tế."*
