# 🔍 Phase 1 — SCAN & Phase 2 — QUICK-ASSESS: Quét Cơ Hội & Đánh Giá Nhanh
## Đơn vị: Vin Smart Future (Vingroup) — Nghiên Cứu Vận Hành VinUni Campus

---

## 🔍 Phase 1 — SCAN: Bảng Quét 5 Bài Toán Thực Tế

Dưới đây là danh sách quét bài toán vận hành sử dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác) trên các đơn vị thành viên Vingroup, tập trung ưu tiên mảng Đời sống & Vận hành Đại học VinUni:

| # | Đơn vị thành viên | Lens áp dụng | Mô tả ngắn gọn bài toán & Điểm nghẽn vận hành |
|---|-------------------|--------------|-----------------------------------------------|
| 1 | **VinUni** (Canteen) | **Lặp lại & Tốn thời gian** | Quy trình điều phối suất ăn 2 chặng: Thanh toán mua vé giấy chung (hoàn toàn KHÔNG ghi món) ──► Cầm vé sang quầy thức ăn xếp hàng lượt 2 ──► Đến lượt mới đứng ngắm khay và chọn đồ ăn trực tiếp. Sinh viên phân vân chọn món làm nghẽn quầy (18-20 phút/lượt), nhà bếp "nấu mù" không dự báo được số lượng suất từng món. |
| 2 | **VinUni** (Thư viện) | **Pain từ người khác** | Tranh chấp và lãng phí phòng học nhóm (Discussion Pods): Tỷ lệ đặt chỗ ảo ("bỏ bom" no-show) lên tới 35%, sinh viên cần phòng thì hệ thống báo hết, thủ thư mất 15-20 phút/lần đi kiểm tra thực địa và can thiệp giải quyết. |
| 3 | **VinUni** (Phòng Đào tạo) | **Lặp lại & AI-upgrade** | Nhân viên Registrar quá tải hàng trăm email/ticket xin đổi lịch thi, rút môn Add/Drop, xin cấp giấy chứng nhận sinh viên đầu kỳ. Mất 12 phút/email tra cứu quy chế lặp đi lặp lại, sinh viên chờ 3-5 ngày mới nhận phản hồi. |
| 4 | **Xanh SM** (GSM) | **Tốn thời gian** | Điều phối viên xử lý thủ công các phản hồi khẩn cấp từ tài xế taxi điện khi pin báo dưới 5% hoặc tìm trạm sạc VinFast còn trụ trống, mất 15 phút tra cứu thủ công toạ độ và tình trạng trụ. |
| 5 | **VinFast** (EV Service) | **AI-upgrade** | Khách hàng mô tả lỗi xe điện bằng tiếng Việt đời thường (ví dụ: *"đi qua gờ giảm tốc bánh trước lục cục"*), nhân viên tiếp nhận mất nhiều thời gian hỏi đi hỏi lại trước khi phân loại đúng mã lỗi kỹ thuật vào xưởng. |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ Bài Toán Tiềm Năng (Quick Problem Cards)

---

### 📌 Thẻ 1: VinUni Canteen — Tối ưu hóa điều phối suất ăn & quy trình order
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
│ AI có thể hỗ trợ ở bước nào? Bước 2 & 4 (Order & chọn món   │
│ trước trên App) & Bước 5 (Dự báo số lượng từng món cho bếp) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian chờ nhận cơm từ 18 phút ──> dưới 3 phút/lượt. │
│ Tỷ lệ thức ăn dư thừa giảm từ 18% ──> dưới 5%.              │
│                                                             │
│ Quick Architecture: [x] LLM Feature + Rule Demand Predictor │
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

## 🗳️ Lựa Chọn Của Nhóm
Nhóm thống nhất chọn **Quick Problem Card #1 (VinUni Canteen)** để tiến hành nghiên cứu sâu trong file `02-deep-dive-report.md`.
