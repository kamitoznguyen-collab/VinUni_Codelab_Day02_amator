# Deep-Dive Report — AI Pre-order & Gợi ý món căn-tin VinUni

## 1. Current-State Workflow

```text
Sinh viên đến căn-tin giờ trưa
  → Xem món/hỏi nhân viên (1–3 phút)
  → Xếp hàng mua vé và thanh toán (5–10 phút) 🔴
      🔄 Sinh viên → thu ngân
  → Nhận vé (1 phút)
  → Xếp hàng lần hai tại quầy cơm (5–10 phút) 🔴
  → Đưa vé, chọn món, nhân viên kiểm tra (1–2 phút)
      🔄 Sinh viên → nhân viên quầy cơm
  → Nhận suất ăn

Tổng cộng giả định: 12–26 phút/lượt vào giờ cao điểm.
```

Các mốc thời gian là giả định scoping, cần đo tại hiện trường trong ít nhất 5 ngày học.

## 2. Problem Statement 6-field

| Field | Nội dung |
|---|---|
| **Actor / Operator** | Sinh viên, thu ngân, nhân viên quầy cơm và quản lý căn-tin. |
| **Current Workflow** | Sinh viên xem món, xếp hàng mua vé/thanh toán, nhận vé rồi xếp hàng tại quầy cơm để đưa vé, chọn món và nhận suất. |
| **Bottleneck** | Hai hàng chờ và hai handoff cho một giao dịch; lịch sử mua/món lưu chưa hỗ trợ quyết định trước giờ cao điểm. |
| **Business Impact** | Ùn tắc, giảm trải nghiệm, tạo áp lực cho nhân viên, giới hạn số suất phục vụ và làm căn-tin khó dự báo nhu cầu từng món. |
| **Success Metric** | Nhận đơn pre-order dưới 5 phút; ≥70% đơn giờ cao điểm qua app/QR; ≥30% dùng đặt lại; đơn sai dưới 2%. |
| **Operational Boundary** | AI chỉ gợi ý và tạo đơn nháp. Không tự đặt, trừ tiền, đổi giá, giữ hàng, tạo QR, hoàn tiền, suy diễn thuộc tính nhạy cảm hoặc đảm bảo dị ứng. Sinh viên xác nhận; nhân viên xử lý ngoại lệ. |

## 3. AI Fit

- **Rule/State-machine:** nguồn sự thật cho menu, giá, tồn kho, giỏ hàng, thanh toán, trạng thái đơn và QR.
- **LLM Feature:** hiểu yêu cầu tự nhiên, gợi ý tối đa 3 món từ menu hợp lệ và tạo đơn nháp.
- **Không dùng Agentic Loop:** AI không cần tự thực hiện chuỗi hành động có tác động tài chính.

## 4. Future-State Flow

```text
Sinh viên mở app/quét QR
  → Hệ thống hiển thị menu, món đã lưu và đơn gần nhất
  → 🔵 AI gợi ý món/tạo đơn nháp
  → Rule engine kiểm tra mã món, giá và tồn kho
  → 🟢 Sinh viên xem đơn và xác nhận thanh toán
  → Cổng thanh toán xử lý → hệ thống tạo QR
  → Quầy nhận đơn
  → 🟢 Nhân viên quét QR và giao món
```

**Fallback:** AI không hiểu thì chuyển sang menu nút bấm; món hết thì rule engine chặn và hiển thị lựa chọn thay thế; thanh toán lỗi thì không tạo đơn; QR lỗi thì tra mã đơn; trường hợp dị ứng thiếu dữ liệu thành phần thì chuyển nhân viên xác minh.

## 5. Prompt Prototype

Prototype tại [`starter-code/prompt_prototype.py`](starter-code/prompt_prototype.py) gọi Gemini 2.5 Flash, ép JSON có cấu trúc và kiểm tra bốn tình huống: vượt bước xác nhận/thanh toán, bịa món và giá, cam kết dị ứng không an toàn, suy diễn tôn giáo từ lịch sử mua.

Kiểm tra cú pháp đã thành công. Live test Gemini chưa chạy vì môi trường hiện chưa có `GEMINI_API_KEY`; không giả lập kết quả mô hình.

## 6. AI Readiness & Decision

| Tiêu chí | Trạng thái | Bằng chứng/việc cần làm |
|---|---|---|
| Có dữ liệu/log sạch | Chưa | Thu thập baseline thời gian chờ, throughput, menu/tồn kho và dữ liệu lịch sử có sự đồng ý. |
| Kiểm soát được rủi ro AI sai | Có | Draft-only, xác nhận người dùng, rule engine cho giao dịch và handoff cho dị ứng/ngoại lệ. |
| Stakeholder sẵn sàng | Chưa xác nhận | Phỏng vấn quản lý, thu ngân, nhân viên quầy và khảo sát sinh viên. |

### Quyết định: NOT YET

Giải pháp có thể prototype nhưng chưa đủ bằng chứng để triển khai thật. Trước khi chuyển sang **GO**, nhóm cần:

1. Đo baseline trong ít nhất 5 ngày học.
2. Chuẩn bị menu/tồn kho mẫu và dữ liệu đã ẩn danh hoặc có sự đồng ý.
3. Chạy đủ bốn adversarial tests với Gemini.
4. Pilot tại một quầy trong 1–2 tuần.

Điều kiện GO đề xuất: nhận đơn pre-order dưới 5 phút, tỷ lệ đơn sai dưới 2%, ít nhất 70% người dùng pilot hoàn thành đặt trước không cần hỗ trợ và 100% test thanh toán/dị ứng vượt qua sau hiệu chỉnh.
