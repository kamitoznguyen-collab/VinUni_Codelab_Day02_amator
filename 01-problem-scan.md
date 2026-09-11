# 📋 Phase 1 — SCAN: Bảng Quét Cơ Hội Bài Toán AI

> **Ngày thực hiện:** 11/09/2026

## 🔍 Hướng tiếp cận
Sử dụng **5 lens** để quét bài toán:
- 🔁 **Lặp lại** — Quy trình rập khuôn, thực hiện hàng trăm lần/ngày
- ⏱️ **Tốn thời gian** — Mất hàng giờ cho tác vụ thủ công
- 😣 **Pain của người khác** — Người vận hành đang chịu quá tải
- 🤖 **AI có thể tốt hơn** — LLM xử lý ngôn ngữ/phi cấu trúc vượt trội hơn rule-based

---

## 📊 Bảng quét 5 bài toán

| # | Ngành / Công ty mẫu | Lens áp dụng | Mô tả ngắn bài toán |
|---|---------------------|-------------|---------------------|
| 1 | **Tuyển dụng Nhân sự** (Headhunt, Doanh nghiệp IT) | 🔁 Lặp lại, 😣 Pain của người khác, ⏱️ Tốn thời gian | **Sàng lọc và trích xuất năng lực ứng viên:** Recruiter mất 2–3 tiếng/ngày đọc lướt hàng trăm CV định dạng khác nhau để bóc tách thông tin (số năm kinh nghiệm, tech stack, chứng chỉ) và đối chiếu với JD, gây quá tải và bỏ sót ứng viên tiềm năng. |
| 2 | **SaaS / Phần mềm Doanh nghiệp** (Base.vn, 1Office) | 🔁 Lặp lại, ⏱️ Tốn thời gian, 😣 Pain của người khác, 🤖 AI upgrade | **Phân loại và định tuyến ticket hỗ trợ kỹ thuật:** Hệ thống rule-based gán nhãn ticket dựa trên danh mục tĩnh (dropdown), nhưng khách thường chọn sai danh mục hoặc viết lỗi mơ hồ ("Phần mềm lag quá"), dẫn đến ticket bị đá qua lại giữa các phòng ban (mất 4–6 tiếng mới tới đúng kỹ sư phụ trách). |
| 3 | **Fintech / Ngân hàng số** (MoMo, Techcombank, MB) | 🔁 Lặp lại, ⏱️ Tốn thời gian, 😣 Pain của người khác, 🤖 AI upgrade | **Đối soát giao dịch treo:** Nhân viên đối soát phải so khớp thủ công mã giao dịch giữa sao kê ngân hàng đối tác và log hệ thống ví khi khách khiếu nại nạp/chuyển tiền bị trừ tiền nhưng chưa nhận (tần suất ~500 ca/ngày, quy trình lặp lại rập khuôn). |
| 4 | **Bảo hiểm** (Prudential, Manulife, Bảo Việt) | 🔁 Lặp lại, ⏱️ Tốn thời gian, 🤖 AI upgrade | **Trích xuất hồ sơ bồi thường (Claim):** Thẩm định viên mất 30–40 phút/hồ sơ để đọc ảnh chụp hóa đơn viện phí viết tay, kết quả xét nghiệm mờ và đối chiếu chéo với danh mục thuốc được chi trả trong hợp đồng. |
| 5 | **Bán lẻ / Chuỗi siêu thị** (WinCommerce, Circle K) | 🔁 Lặp lại, ⏱️ Tốn thời gian | **Quản lý hàng cận date:** Nhân viên ca tối phải đi quét mắt từng kệ để nhặt hàng sắp hết hạn, tính toán tỷ lệ giảm giá theo rule (10%–30%–50%), in tem mới và nhập danh sách hủy hàng vào ERP thủ công. |

---

# 🎯 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

## Quick Problem Card #1 — Tuyển dụng IT

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 — Tuyển dụng IT                       │
│                                                             │
│ Bài toán: Chuyên viên tuyển dụng (IT Recruiter) mất quá     │
│ nhiều thời gian đọc và bóc tách năng lực kỹ thuật từ hàng    │
│ trăm CV có cấu trúc lộn xộn để so khớp với JD.              │
│ Đơn vị áp dụng: Bộ phận Talent Acquisition / Công ty IT      │
│                                                             │
│ Ai đang đau? IT Recruiter (quá tải), Hiring Manager (chờ lâu)│
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tải CV từ các nguồn (TopCV, LinkedIn, Email)           │
│   → 2. Đọc lướt tìm Tech Stack, số năm kinh nghiệm, dự án   │
│   → 3. So khớp thủ công từng tiêu chí với Job Description   │
│   → 4. Nhập tay thông tin tóm tắt vào bảng theo dõi ATS     │
│   → 5. Soạn email thông báo Pass/Fail cho ứng viên           │
│                                                             │
│ Bước nào tốn nhất? Bước 2 & 3 (⏱ 12–15 phút/CV)             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 & 4         │
│ (Trích xuất JSON cấu trúc → Chấm điểm match → Draft tóm tắt)│
│                                                             │
│ Đo thành công bằng gì?                                      │
│ Giảm thời gian sàng lọc 1 CV từ 18 phút → dưới 3 phút.     │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Structured Extraction) │
└─────────────────────────────────────────────────────────────┘
```

---

## Quick Problem Card #2 — Phân loại Ticket hỗ trợ kỹ thuật

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 — Phân loại Ticket SaaS               │
│                                                             │
│ Bài toán: Hệ thống rule-based gán nhãn ticket dựa trên      │
│ dropdown tĩnh, nhưng khách thường chọn sai hoặc mô tả mơ   │
│ hồ, dẫn đến ticket bị đá qua lại giữa các phòng ban.       │
│ Đơn vị áp dụng: Phòng CSKH / SaaS (Base.vn, 1Office)       │
│                                                             │
│ Ai đang đau? Nhân viên Support L1, khách hàng (chờ lâu)     │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách tạo ticket qua portal (chọn dropdown)            │
│   → 2. L1 đọc nội dung, đoán phòng ban phụ trách            │
│   → 3. Chuyển ticket → nếu sai → đá lại → lặp lại          │
│   → 4. Kỹ sư đúng tiếp nhận và xử lý                       │
│                                                             │
│ Bước nào tốn nhất? Bước 2 & 3 (⏱ 4–6 tiếng/ticket vòng đời)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2               │
│ (NLP phân loại nội dung ticket → gán nhãn phòng ban)        │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ Giảm tỷ lệ ticket bị chuyển sai phòng ban từ 35% → <5%.    │
│ Giảm thời gian routing trung bình từ 5h → <30 phút.        │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Text Classification)   │
└─────────────────────────────────────────────────────────────┘
```

---

## Quick Problem Card #3 — Đối soát giao dịch treo (Fintech)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 — Đối soát giao dịch treo             │
│                                                             │
│ Bài toán: Nhân viên đối soát phải so khớp thủ công mã giao │
│ dịch giữa sao kê ngân hàng đối tác và log hệ thống ví      │
│ khi khách khiếu nại nạp/chuyển tiền bị trừ nhưng chưa nhận.│
│ Đơn vị áp dụng: Fintech / Ngân hàng số (MoMo, MB)          │
│                                                             │
│ Ai đang đau? Nhân viên đối soát (quá tải 500 ca/ngày),     │
│ khách hàng (chờ hoàn tiền lâu)                              │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhận khiếu nại từ khách (mã GD, số tiền, thời gian)   │
│   → 2. Mở sao kê ngân hàng đối tác, tìm mã giao dịch      │
│   → 3. So khớp với log hệ thống ví nội bộ                   │
│   → 4. Xác nhận trạng thái & xử lý hoàn tiền/credit        │
│                                                             │
│ Bước nào tốn nhất? Bước 2 & 3 (⏱ 10–15 phút/ca)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3           │
│ (OCR sao kê + Matching tự động mã giao dịch)               │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ Giảm thời gian xử lý 1 ca từ 15 phút → dưới 2 phút.       │
│ Tỷ lệ matching chính xác đạt ≥ 98%.                        │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Entity Matching + OCR) │
└─────────────────────────────────────────────────────────────┘
```
