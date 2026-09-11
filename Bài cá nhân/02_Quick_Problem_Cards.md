
# Quick Problem Cards — Vin Smart Future

> **Lưu ý về dữ liệu:** Các số liệu trong ba card là giả định ban đầu phục vụ bài lab, chưa phải số liệu nội bộ đã được xác nhận. Khi làm Deep-Dive, cần ghi rõ đây là baseline cần đo lại bằng dữ liệu thật.

---

## QUICK PROBLEM CARD #1 — VinFast

### Bài toán

Chuẩn hóa yêu cầu đặt lịch sửa chữa/bảo dưỡng xe VinFast và đề xuất trước loại dịch vụ, thông tin cần bổ sung và checklist phụ tùng cho xưởng.

### Công ty thành viên

- [x] VinFast
- [ ] Xanh SM
- [ ] Vinhomes
- [ ] Vinmec

### Ai đang đau? — Actor

- Khách hàng: phải gọi lại nhiều lần để bổ sung thông tin lỗi xe.
- Cố vấn dịch vụ: phải đọc mô tả tự do và hỏi lại các dữ kiện cần thiết.
- Xưởng dịch vụ: có thể chuẩn bị thiếu phụ tùng hoặc phân công sai loại kỹ thuật viên.

### Workflow thủ công hiện tại

1. Khách hàng gửi yêu cầu qua ứng dụng, hotline hoặc trực tiếp tại xưởng.
2. Cố vấn dịch vụ đọc mô tả lỗi và gọi lại hỏi thêm dòng xe, triệu chứng, thời điểm phát sinh.
3. Cố vấn xác định loại dịch vụ: bảo dưỡng, sửa chữa tại xưởng hoặc Mobile Service.
4. Xưởng kiểm tra lịch trống và dự đoán phụ tùng/kỹ thuật viên cần chuẩn bị.
5. Nhân viên xác nhận lịch hẹn với khách hàng.

### Bước nào tốn thời gian/lỗi nhất?

**Bước 2–4** là bottleneck: mất khoảng **8–12 phút/yêu cầu** để chuẩn hóa mô tả lỗi và chuẩn bị lịch. Ước tính **10–20% yêu cầu** phải gọi lại do thiếu thông tin; **5–10% lịch hẹn** có thể phải điều chỉnh vì chuẩn bị chưa đúng phụ tùng hoặc loại kỹ thuật viên.

### AI có thể hỗ trợ ở bước nào?

AI có thể đọc mô tả tiếng Việt, trích xuất dòng xe, biển số, triệu chứng, mức độ khẩn cấp và đề xuất loại dịch vụ. AI cũng có thể tạo checklist câu hỏi bổ sung và checklist phụ tùng dạng nháp cho cố vấn dịch vụ.

### Đo thành công bằng gì? — Metric

- Giảm thời gian chuẩn hóa một yêu cầu từ **8–12 phút xuống dưới 2 phút**.
- Đạt ít nhất **90% độ chính xác** khi trích xuất các trường thông tin bắt buộc.
- Giảm tỷ lệ phải gọi lại để hỏi thông tin từ **10–20% xuống dưới 5%**.

### Operational Boundary sơ bộ

AI chỉ được tạo bản nháp và đề xuất. AI **không được tự kết luận xe an toàn/không an toàn, tự báo giá, tự xác nhận lịch hoặc tự quyết định thay thế phụ tùng**. Cố vấn dịch vụ hoặc kỹ thuật viên phải phê duyệt.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] LLM Feature + Rule kiểm tra trường bắt buộc
- [ ] Agent

---

## QUICK PROBLEM CARD #2 — Vinmec

### Bài toán

Kiểm tra thông tin còn thiếu và chuẩn hóa yêu cầu đặt lịch khám của bệnh nhân trước khi nhân viên tổng đài gọi lại xác nhận.

### Công ty thành viên

- [ ] VinFast
- [ ] Xanh SM
- [ ] Vinhomes
- [x] Vinmec

### Ai đang đau? — Actor

- Bệnh nhân/người đặt lịch: phải trao đổi nhiều lần nếu điền thiếu hoặc sai thông tin.
- Nhân viên tổng đài: phải kiểm tra thủ công cơ sở, chuyên khoa, bác sĩ và thời gian mong muốn.
- Bộ phận tiếp đón: nhận được yêu cầu chưa đầy đủ hoặc không nhất quán.

### Workflow thủ công hiện tại

1. Bệnh nhân nhập yêu cầu đặt lịch trên website, ứng dụng hoặc gọi tổng đài.
2. Nhân viên kiểm tra họ tên, số điện thoại, cơ sở, chuyên khoa/bác sĩ và thời gian mong muốn.
3. Nhân viên gọi lại nếu thông tin thiếu, mâu thuẫn hoặc bệnh nhân chọn chưa đúng cơ sở.
4. Nhân viên kiểm tra lịch trống và xác nhận lịch khám.
5. Hệ thống gửi thông tin xác nhận cho bệnh nhân.

### Bước nào tốn thời gian/lỗi nhất?

**Bước 2–3** là bottleneck: mất khoảng **3–7 phút/yêu cầu** để kiểm tra và gọi lại. Ước tính **10–15% yêu cầu** cần liên hệ lại nhiều lần; **5–10% lịch hẹn** có thể phải thay đổi do thông tin ban đầu chưa đầy đủ.

### AI có thể hỗ trợ ở bước nào?

AI có thể kiểm tra biểu mẫu, phát hiện trường còn thiếu, chuẩn hóa cách viết tên chuyên khoa/cơ sở và tạo tin nhắn yêu cầu bệnh nhân bổ sung thông tin. AI chỉ hỗ trợ điều phối hành chính, không chẩn đoán bệnh.

### Đo thành công bằng gì? — Metric

- Giảm thời gian kiểm tra ban đầu từ **3–7 phút xuống dưới 1 phút/yêu cầu**.
- Đạt ít nhất **95% độ chính xác** khi phát hiện trường thông tin còn thiếu.
- Giảm số yêu cầu phải gọi lại nhiều lần từ **10–15% xuống dưới 5%**.

### Operational Boundary sơ bộ

AI **không được chẩn đoán, tư vấn điều trị, tự đánh giá mức độ bệnh hoặc tự quyết định chuyên khoa trong tình huống khẩn cấp**. Mọi lịch khám phải được nhân viên Vinmec kiểm tra và xác nhận; dữ liệu sức khỏe phải được bảo vệ và chỉ dùng đúng mục đích.

### Quick Architecture

- [ ] No AI
- [x] Rule + LLM Feature
- [ ] Agent

---

## QUICK PROBLEM CARD #3 — Vinhomes

### Bài toán

Kiểm tra tính đầy đủ và mức độ tuân thủ quy định của hồ sơ đăng ký thi công nội thất trước khi Ban Quản lý phê duyệt.

### Công ty thành viên

- [ ] VinFast
- [ ] Xanh SM
- [x] Vinhomes
- [ ] Vinmec

### Ai đang đau? — Actor

- Cư dân/chủ căn hộ: phải bổ sung hồ sơ nhiều lần và chờ phản hồi.
- Nhân viên Ban Quản lý: phải đọc phương án thi công, kiểm tra giấy tờ và đối chiếu nhiều quy định.
- Đội bảo vệ/kỹ thuật: cần biết lịch thi công, người ra vào và việc vận chuyển vật liệu.

### Workflow thủ công hiện tại

1. Cư dân hoặc nhà thầu gửi đơn đăng ký, phương án thi công và giấy tờ liên quan.
2. Nhân viên Ban Quản lý đọc và kiểm tra thủ công từng hồ sơ.
3. Nhân viên đối chiếu thời gian thi công, quy định về tiếng ồn, vận chuyển vật liệu và thông tin nhà thầu.
4. Nhân viên yêu cầu bổ sung/chỉnh sửa nếu hồ sơ thiếu hoặc chưa phù hợp.
5. Ban Quản lý phê duyệt và thông báo lịch cho bảo vệ, kỹ thuật và cư dân.

### Bước nào tốn thời gian/lỗi nhất?

**Bước 2–4** là bottleneck: mất khoảng **10–20 phút/hồ sơ** để kiểm tra. Ước tính **15–25% hồ sơ** phải bổ sung hoặc chỉnh sửa; thời gian chờ phê duyệt có thể kéo dài thêm **1–3 ngày** nếu hồ sơ bị trả lại nhiều lần.

### AI có thể hỗ trợ ở bước nào?

AI có thể đọc biểu mẫu và tài liệu đính kèm, kiểm tra các trường bắt buộc, tóm tắt kế hoạch thi công, phát hiện lịch thi công ngoài khung giờ cho phép và tạo danh sách điểm cần nhân viên xem xét.

### Đo thành công bằng gì? — Metric

- Giảm thời gian kiểm tra hồ sơ từ **10–20 phút xuống dưới 3 phút/hồ sơ**.
- Đạt ít nhất **90% độ chính xác** khi phát hiện trường thông tin hoặc giấy tờ còn thiếu.
- Giảm tỷ lệ hồ sơ phải bổ sung từ **15–25% xuống dưới 10%**.

### Operational Boundary sơ bộ

AI chỉ được kiểm tra, tóm tắt và đề xuất. AI **không được tự phê duyệt thi công, tự cấp quyền ra vào, tự kết luận trách nhiệm pháp lý hoặc tự gửi thông báo phê duyệt**. Ban Quản lý phải duyệt cuối cùng.

### Quick Architecture

- [ ] No AI
- [x] Rule + LLM Feature
- [ ] Agent

---

## Gợi ý lựa chọn để làm Deep-Dive

Nếu cần chọn một card để phát triển tiếp, ưu tiên **Card #3 — Vinhomes kiểm tra hồ sơ đăng ký thi công nội thất** vì:

1. Khác rõ với pain point mẫu về phân loại khiếu nại cư dân.
2. Quy trình có đầu vào, bottleneck, người phê duyệt và đầu ra cụ thể.
3. Có thể dùng LLM để đọc hiểu hồ sơ nhưng vẫn giữ Human-in-the-loop.
4. Rủi ro thấp hơn các bài toán chẩn đoán y tế hoặc kết luận an toàn xe.
