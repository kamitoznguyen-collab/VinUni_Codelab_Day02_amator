# 📓 Nhật ký tương tác AI — AI Log & Reflection

> **Ngày thực hiện:** 11/09/2026
> **Công cụ AI sử dụng:** Claude (Anthropic), Gemini (Google)

---

## 1. AI giúp gì trong quá trình làm bài?

### 1.1. Brainstorm bài toán (Phase 1 — SCAN)
- **Prompt gửi AI:** Yêu cầu AI gợi ý 5 bài toán vận hành thực tế có thể tối ưu bằng AI trong các ngành: Tuyển dụng IT, SaaS, Fintech, Bảo hiểm, Bán lẻ.
- **AI giúp được:** Liệt kê nhanh các pain point phổ biến, bổ sung góc nhìn về tần suất lặp lại và business impact bằng con số cụ thể.
- **Hạn chế:** Một số con số thống kê AI đưa ra (ví dụ: "30% ứng viên bỏ lỡ") có thể là hallucination — cần cross-check với dữ liệu thực tế.

### 1.2. Phân tích sâu bài toán (Phase 3 — DEEP-DIVE)
- **Prompt gửi AI:** Yêu cầu AI phân tích chi tiết workflow sàng lọc CV hiện tại, xác định bottleneck và đề xuất future-state flow có AI.
- **AI giúp được:** Cấu trúc hóa problem statement theo 6 trường (Actor, Workflow, Bottleneck, Impact, Metric, Boundary) rất nhanh và logic.
- **Hạn chế:** AI ban đầu không nhấn mạnh đủ mạnh về Operational Boundary (Anti-Bias), phải prompt lại để bổ sung rõ ràng hơn.

### 1.3. Thiết kế Adversarial Test (Phase 4)
- **Prompt gửi AI:** Yêu cầu AI viết kịch bản tấn công prompt injection cho bài toán CV screening.
- **AI giúp được:** Tạo ra các kịch bản tấn công sáng tạo (tiêm lệnh vào phần kinh nghiệm CV) mà bản thân mình chưa nghĩ tới.

---

## 2. AI trả lời sai / hallucination ở đâu?

| Lần | Nội dung sai | Cách phát hiện | Cách sửa |
|-----|-------------|---------------|---------|
| 1 | AI đưa con số "30% ứng viên chất lượng cao nhận offer nơi khác" — có thể không chính xác cho mọi công ty | Kiểm tra lại với báo cáo LinkedIn Talent Trends | Giữ con số nhưng ghi chú "ước tính trung bình ngành" |
| 2 | AI ban đầu đề xuất dùng Agent tự hành cho CV screening | Nhận ra rủi ro đạo đức tuyển dụng nếu AI tự quyết | Sửa lại thành LLM Feature (chỉ trích xuất, không quyết định) |
| 3 | AI đề xuất dùng "năm sinh" để tính số năm kinh nghiệm | Vi phạm Anti-Bias — không được dùng thông tin nhân khẩu học | Sửa prompt boundary: CẤM dùng năm sinh, giới tính, quê quán |

---

## 3. Bài học rút ra

1. **AI là trợ lý draft, không phải người ra quyết định.** Mọi output cần gắn tag `[DRAFT]` và phải có human review.
2. **Prompt boundary quan trọng hơn prompt chính.** Nếu không có ranh giới rõ ràng, AI sẽ dễ bị "social engineering" qua dữ liệu đầu vào.
3. **Luôn stress-test bằng adversarial input** trước khi đưa vào production — đặc biệt với bài toán liên quan đến con người (tuyển dụng, y tế).
4. **Cross-check con số thống kê** — AI hay "tự tin" đưa ra con số cụ thể nhưng không phải lúc nào cũng có nguồn đáng tin cậy.
