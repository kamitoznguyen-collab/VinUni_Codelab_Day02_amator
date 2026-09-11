# AI Log & Reflection — Lab 02: AI Product Scoping

## 1. Bối cảnh sử dụng AI

Trong buổi Lab, tôi sử dụng AI như một thought-partner trong vai trò AI Engineer tại Vin Smart Future. Tôi không giao cho AI quyết định thay mình, mà dùng AI để brainstorm pain point, phản biện ý tưởng, cấu trúc hóa quy trình và kiểm tra các ranh giới an toàn của prototype.

Use case tôi tập trung phân tích là **Vinhomes — kiểm tra tính đầy đủ và mức độ tuân thủ của hồ sơ đăng ký thi công nội thất** trước khi Ban Quản lý phê duyệt.

Các con số về số lượng hồ sơ, thời gian xử lý và tỷ lệ hồ sơ phải bổ sung trong bài là **ước tính phục vụ bài lab**, không phải số liệu nội bộ đã được Vinhomes xác nhận.

---

## 2. AI đã giúp tôi những gì?

### 2.1. Mở rộng không gian tìm kiếm vấn đề

AI giúp tôi liệt kê các pain point vận hành ở nhiều công ty thành viên như VinFast, Xanh SM, Vinhomes và Vinmec. Nhờ đó, tôi không bị giới hạn ở một ý tưởng đầu tiên mà có thể so sánh nhiều loại quy trình:

- VinFast: chuẩn hóa yêu cầu đặt lịch sửa chữa và chuẩn bị phụ tùng.
- Vinmec: kiểm tra thông tin còn thiếu khi đặt lịch khám.
- Vinhomes: kiểm tra hồ sơ đăng ký thi công nội thất.

Điều quan trọng là AI giúp tôi nhìn pain point theo quy trình và bottleneck, thay vì chỉ nghĩ đến một chatbot chung chung.

### 2.2. Chuyển ý tưởng thành Quick Problem Card

AI giúp tôi điền các trường bắt buộc trong Quick Problem Card:

- Actor đang gặp khó khăn.
- Các bước của workflow hiện tại.
- Bước nào tốn thời gian hoặc dễ sai.
- AI có thể tham gia ở bước nào.
- Metric có số để đo thành công.
- Operational Boundary và Human-in-the-loop.

Ví dụ, thay vì viết mơ hồ rằng “AI hỗ trợ Ban Quản lý Vinhomes”, tôi cụ thể hóa thành: AI đọc hồ sơ, kiểm tra trường bắt buộc, phát hiện lịch thi công ngoài quy định và tạo danh sách điểm cần nhân viên xem xét.

### 2.3. Giúp tôi nhận ra giải pháp không nhất thiết phải là Agent

Qua quá trình phản biện, tôi nhận ra bài toán kiểm tra hồ sơ thi công có quy trình cố định. Vì vậy, giải pháp phù hợp hơn là kết hợp **Rule + LLM Feature**:

- Rule kiểm tra các điều kiện rõ ràng như trường bắt buộc và khung giờ thi công.
- LLM đọc hiểu nội dung tự do trong phương án thi công và tóm tắt tài liệu.
- Nhân viên Ban Quản lý phê duyệt cuối cùng.

Dùng một Agent tự trị để tự phê duyệt hoặc cấp quyền ra vào sẽ làm rủi ro tăng lên mà không tạo thêm giá trị tương xứng.

### 2.4. Hỗ trợ thiết kế prototype và adversarial tests

Đối với file `prompt_prototype.py`, AI giúp tôi thiết kế:

- System prompt quy định rõ vai trò và ranh giới vận hành.
- JSON schema để output có cấu trúc.
- Nhãn `[DRAFT_ONLY]` nhằm ngăn việc gửi tin nhắn tự động.
- Ba adversarial test để kiểm tra việc bỏ qua ranh giới, prompt injection và tình huống pin xe dưới 5%.

AI cũng gợi ý thêm lớp kiểm tra sau khi model trả lời. Điều này giúp tôi hiểu rằng không nên chỉ tin vào system prompt; các quy tắc quan trọng cần được kiểm tra bằng code hoặc workflow của hệ thống.

---

## 3. AI đã sai hoặc tạo ra rủi ro ở đâu?

### 3.1. Ý tưởng ban đầu quá giống ví dụ có sẵn

Ban đầu tôi chọn bài toán Vinhomes “phân loại và điều hướng phản ánh cư dân”. Sau khi đối chiếu với Inspiration Kit, tôi nhận ra ý tưởng này gần như trùng với pain point mẫu. Nếu giữ nguyên, bài làm sẽ thiếu tính độc lập.

Tôi đã sửa hướng bằng cách chọn một quy trình khác: kiểm tra hồ sơ đăng ký thi công nội thất. Pain point mới có workflow, người phê duyệt và ranh giới rõ hơn.

### 3.2. Các con số ước tính có thể bị hiểu nhầm là sự thật

AI từng đưa ra các con số như số lượng yêu cầu mỗi ngày, số phút xử lý và tỷ lệ chuyển sai. Những con số này nghe hợp lý nhưng không thể xem là dữ liệu thật nếu chưa có log vận hành.

Tôi đã sửa bằng cách:

- Ghi rõ “ước tính phục vụ bài lab”.
- Không dùng các con số đó để khẳng định hiệu quả thực tế của Vinhomes.
- Đưa việc đo baseline thật vào phần Evaluate.
- Chỉ coi các metric này là giả thuyết cần kiểm chứng bằng dữ liệu.

### 3.3. Có sự không nhất quán giữa use case và code starter

Use case báo cáo của tôi là Vinhomes, nhưng `starter-code/prompt_prototype.py` và autograder được thiết kế cứng cho use case Xanh SM với các luật `DRAFT_ONLY`, pin dưới 5% và `dispatch_mobile_charger`.

Nếu không kiểm tra kỹ, tôi có thể viết báo cáo về Vinhomes nhưng lại trình bày prototype Xanh SM như thể chúng là cùng một sản phẩm. Tôi đã ghi nhận đây là một điểm lệch phạm vi:

- Báo cáo scoping cần mô tả đúng use case mà nhóm lựa chọn.
- Code starter hiện phục vụ bài prototype cá nhân theo ranh giới Xanh SM.
- Khi nhóm chốt use case cuối cùng, cần quyết định rõ có xây prototype Vinhomes riêng hay tiếp tục dùng prototype Xanh SM theo yêu cầu autograder.

### 3.4. AI không tự phát hiện mọi lỗi dữ liệu

Trong quá trình rà soát file scan, tôi phát hiện một dòng mô tả yêu cầu bảo hành của Vinhomes bị gán nhầm công ty thành Vinmec. Đây là lỗi nhập liệu/kiểm tra, không phải lỗi cú pháp.

Điều này cho tôi thấy rằng AI có thể giúp tạo nội dung nhanh nhưng người làm vẫn phải kiểm tra các trường quan trọng như tên công ty, actor, workflow và nguồn dữ liệu.

---

## 4. Tôi đã sửa prompt và ranh giới như thế nào?

Tôi đã chuyển từ prompt chung chung sang prompt có cấu trúc và có điều kiện kiểm soát:

1. Nêu rõ vai trò của AI và người chịu trách nhiệm cuối cùng.
2. Tách nhiệm vụ được phép làm khỏi nhiệm vụ bị cấm.
3. Yêu cầu output có JSON schema cố định thay vì văn bản tự do.
4. Bắt buộc phản hồi ở trạng thái draft và có Human-in-the-loop.
5. Quy định fallback khi thiếu dữ liệu hoặc model không chắc chắn.
6. Viết adversarial tests để thử các tình huống người dùng yêu cầu bỏ qua system prompt.
7. Thêm kiểm tra sau output để chặn hành động nguy hiểm ngay cả khi model trả lời sai.

Đối với bài toán Vinhomes, ranh giới tương ứng là:

- AI được phép kiểm tra tính đầy đủ của hồ sơ.
- AI được phép tóm tắt phương án và đánh dấu điểm có khả năng vi phạm quy định.
- AI không được tự phê duyệt thi công.
- AI không được tự cấp quyền ra vào hoặc thông báo rằng hồ sơ đã được duyệt.
- Hồ sơ thiếu dữ liệu phải chuyển cho nhân viên xử lý thủ công.

---

## 5. Bài học cá nhân

Bài học lớn nhất của tôi là **Problem First, AI Second**. Tôi không nên bắt đầu bằng câu hỏi “Dùng Agent nào cho bài toán này?”, mà phải bắt đầu từ workflow hiện tại, bottleneck, chi phí và quyền hạn của từng actor.

Tôi cũng hiểu rõ hơn rằng một prototype AI tốt không chỉ là gọi API thành công. Prototype phải thể hiện được:

- Input nào được chấp nhận.
- Output có cấu trúc ra sao.
- AI được phép làm gì.
- AI tuyệt đối không được làm gì.
- Con người duyệt ở bước nào.
- Hệ thống làm gì khi AI sai hoặc thiếu dữ liệu.

Sau buổi học, tôi tự tin hơn trong việc dùng AI để suy nghĩ và phản biện. Tuy nhiên, tôi cũng nhận thức rõ rằng AI không thể thay thế việc xác minh dữ liệu, kiểm tra quy trình thực tế và chịu trách nhiệm về quyết định vận hành.

---

## 6. Tự đánh giá

Tôi đánh giá mức độ phối hợp với AI của mình là **4/5**.

AI giúp tôi tiết kiệm nhiều thời gian trong việc brainstorm và cấu trúc hóa ý tưởng. Tôi chưa đánh giá 5/5 vì vẫn cần cải thiện khả năng kiểm chứng số liệu, giữ tính nhất quán giữa báo cáo và prototype, cũng như kiểm tra kỹ hơn tên công ty và nguồn của từng giả định.
