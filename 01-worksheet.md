# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**.

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:

- 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
- 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
- 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
- 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
- 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate                         | Điểm | Deliverable       | Tiêu chí chấm                                                                |
| ---------------------------- | ---: | ----------------- | ---------------------------------------------------------------------------- |
| **G1. Workflow Mapping**     |   20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck     |
| **G2. Problem Statement**    |   20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** |   10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback  |
| **G4. Decision Quality**     |   10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng                |

### 👤 Điểm cá nhân (40 điểm)

| Gate                        | Điểm | Deliverable  | Tiêu chí chấm                                                                     |
| --------------------------- | ---: | ------------ | --------------------------------------------------------------------------------- |
| **I1. Scan & Cards**        |   15 | Quick Cards  | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng          |
| **I2. Prototyping**         |   10 | 02-lab/      | Chạy thử nghiệm programmatic prompt prototype thành công                          |
| **I3. AI Log & Reflection** |   15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

_Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI._
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:

1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> _"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."_

### 📝 List bài toán của tôi:

| #   | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
| --- | ------------------------------- | ---- | ------------------- |
| 1 | VinUni Canteen | Tốn thời gian | Sinh viên phải xếp hàng mua vé rồi xếp hàng lần hai ở quầy cơm vào giờ trưa. |
| 2 | VinUni Canteen | Lặp lại | Thu ngân và nhân viên quầy cơm lặp lại việc thu tiền, kiểm tra vé và xác nhận món cho từng suất ăn. |
| 3 | VinUni Canteen | AI có thể tốt hơn | Menu chưa tận dụng lịch sử mua và món đã lưu để giúp sinh viên đặt lại hoặc khám phá món phù hợp. |
| 4 | Vinhomes | AI có thể tốt hơn | Điều hòa, chiếu sáng và bơm nước có thể vận hành theo lịch cố định thay vì theo mức sử dụng thực tế. |
| 5 | Vinhomes | Tốn thời gian | Bảo vệ phải theo dõi nhiều luồng camera để phát hiện xe đỗ sai, khu vực đông bất thường hoặc vật thể bỏ quên. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #___                                     │
│                                                             │
│ Bài toán (1 câu): ________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? ______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. ___ ──> 2. ___ ──> 3. ___ ──> 4. ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ___ (⏱ ___ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? _____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? ______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #1 — Căn-tin VinUni

| Trường | Nội dung |
|---|---|
| **Bài toán** | Sinh viên phải mua vé rồi xếp hàng lần hai để nhận cơm vào giờ trưa, trong khi lịch sử món ăn chưa được dùng để đặt lại hay gợi ý món mới. |
| **Công ty thành viên** | Khác: VinUni Canteen (hệ sinh thái Vingroup). |
| **Ai đang đau?** | Sinh viên, thu ngân, nhân viên quầy cơm và quản lý căn-tin. |
| **Workflow hiện tại** | Xem món → xếp hàng mua vé/thanh toán → nhận vé → xếp hàng ở quầy cơm → đưa vé, chọn món và nhận suất. |
| **Bước tốn thời gian/lỗi nhất** | Hai hàng chờ tại quầy vé và quầy cơm; khoảng 10–20 phút chờ vào giờ cao điểm. |
| **AI hỗ trợ tại đâu?** | Hiểu yêu cầu món ăn, gợi ý món từ lịch sử/món đã lưu, tạo đơn nháp và đề xuất món thay thế khi món hết. |
| **Metric** | Đơn đặt trước hoàn tất trong dưới 5 phút; ≥70% đơn giờ cao điểm qua app/QR; tỷ lệ đơn sai dưới 2%. |
| **Quick Architecture** | `[x] Rule / State-machine` + `[x] LLM Feature`; không dùng Agentic Loop. |

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> _"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."_

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## Bài toán: AI Pre-order & Gợi ý món cá nhân hóa cho căn-tin VinUni

Mục tiêu là loại bỏ bước mua vé, cho phép sinh viên lưu món quen, đặt lại nhanh và nhận gợi ý món mới phù hợp.

## 3.1. Current-State Workflow Mapping

```text
Sinh viên đến căn-tin giờ trưa
  → [1] Xem món / hỏi nhân viên / suy nghĩ chọn món (1–3 phút)
  → [2] Xếp hàng mua vé và thanh toán (5–10 phút) 🔴
      🔄 Handoff: sinh viên → thu ngân
  → [3] Nhận vé (1 phút)
  → [4] Xếp hàng lần hai tại quầy cơm (5–10 phút) 🔴
  → [5] Đưa vé, chọn món, nhân viên kiểm tra vé (1–2 phút)
      🔄 Handoff: sinh viên → nhân viên quầy cơm
  → [6] Nhận suất ăn

Tổng cộng = khoảng 12–26 phút/lượt vào giờ cao điểm.
```

## 3.2. Problem Statement (6-field) & Metrics

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Sinh viên; thu ngân; nhân viên phục vụ quầy cơm; quản lý căn-tin. |
| **2. Current Workflow** | Sinh viên xem món tại chỗ, xếp hàng mua vé/thanh toán, nhận vé, rồi xếp hàng tại quầy cơm để đưa vé, chọn món và nhận suất. Lịch sử món đã mua chưa được tận dụng để đặt lại hoặc gợi ý. |
| **3. Bottleneck** | Sinh viên phải quyết định món vào giờ đông và xếp hàng hai lần. Nhân viên mất thời gian thu tiền, kiểm tra vé và trả lời các câu hỏi lặp lại về món. |
| **4. Business Impact** | Hàng chờ dài gây ùn tắc và giảm trải nghiệm giờ trưa; căn-tin phục vụ được ít suất hơn trong thời gian giới hạn và khó dự báo nhu cầu từng món. Cần đo baseline thực tế trước pilot. |
| **5. Success Metric** | Đơn đặt trước hoàn tất trong dưới 5 phút; ≥70% đơn giờ cao điểm qua app/QR; ≥30% người dùng dùng “Đặt lại món quen”; tỷ lệ đơn sai dưới 2%. |
| **6. Operational Boundary** | AI chỉ dùng lịch sử đơn, món đã lưu và sở thích do sinh viên tự khai để gợi ý/tạo đơn nháp. AI không được tự đặt món, tự trừ tiền, suy diễn dị ứng/sức khỏe/tôn giáo hoặc tự hoàn tiền. Sinh viên xác nhận thanh toán; nhân viên/quản lý xử lý đơn lỗi, hết món, khiếu nại và hoàn tiền. |

## 3.3. Future-State Flow & AI Fit

**AI Fit:** `[x] Rule / State-Machine` + `[x] LLM Feature` ; `[ ] Agentic Loop`.

- **Rule/State-machine:** menu, giá, tồn món, giỏ hàng, thanh toán và QR nhận món.
- **LLM Feature:** hiểu yêu cầu tự nhiên, gợi ý món từ lịch sử/món đã lưu/ngân sách và đề xuất món thay thế.
- **Không dùng Agentic Loop:** tạo đơn và thanh toán phải do sinh viên chủ động xác nhận.

```text
Sinh viên mở app / quét QR
  → Hiển thị món đã lưu và “Đặt lại đơn gần nhất”
  → 🔵 AI gợi ý món mới theo menu hôm nay và lịch sử mua
  → Rule kiểm tra giá, món còn/hết và thời gian nhận
  → 🟢 Sinh viên xem giỏ, xác nhận thanh toán
  → Cổng thanh toán thành công → tạo QR/mã nhận món
  → Đơn chuyển tới quầy cơm
  → 🟢 Nhân viên quét QR và giao món
```

**↩️ Fallback:** AI không hiểu/gợi ý không phù hợp thì sinh viên tự chọn menu; món hết thì hiển thị món thay thế; thanh toán lỗi thì không tạo đơn và cho phép thanh toán lại/tới quầy; QR lỗi thì nhân viên tra mã đơn. Với chế độ ăn/dị ứng, chỉ hiện thông tin sinh viên tự khai và nhắc kiểm tra thành phần món.

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:

1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   - **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   - **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   - **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:

1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**

> _Viết lý giải chi tiết tại đây_

---

# 📝 Phase 6 — REFLECTION (Cá nhân)

_Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`._
