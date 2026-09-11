# 📋 Báo Cáo Phân Tích Sâu (Deep-Dive Report) — Vin Smart Future
## Dự Án: Ứng Dụng VinUni Smart Canteen App & Trợ Lý AI Gợi Ý Món Ăn Theo Thói Quen

> **Môn học:** AI Product Scoping (Vin Smart Future — Lab 02)  
> **Đơn vị phụ trách:** Vin Smart Future (Vingroup) — Chi nhánh VinUni Campus  
> **Thành viên thực hiện:** Duy (Nhóm Kỹ sư AI Product Vin Smart Future)  
> **Mảng hoạt động:** Giáo dục đại học & Dịch vụ đời sống sinh viên (VinUni Campus Life & Dining Services)

---

## 🏛️ 1. Bối cảnh & Lý do lựa chọn bài toán

### 1.1. Bối cảnh vận hành tại VinUni
Đại học VinUni tại khu đô thị Vinhomes Ocean Park quy tụ hơn 1.500 sinh viên, giảng viên và cán bộ nhân viên. Khu vực Canteen trung tâm là nơi phục vụ ăn trưa chính với khung giờ cao điểm tập trung từ **11h45 đến 12h30** mỗi ngày.

Hiện tại, quy trình phục vụ tại canteen vận hành theo mô hình thủ công qua 2 chặng: **Xếp hàng thanh toán mua vé ăn chung (vé giấy chỉ có mệnh giá, hoàn toàn KHÔNG ghi món ăn cụ thể) ──► Cầm vé giấy sang quầy thức ăn xếp hàng lượt 2 ──► Đến lượt mới đứng ngắm khay và chọn đồ ăn trực tiếp ──► Nhân viên xé vé và xúc món**.

### 1.2. Quyết định lựa chọn từ Phase 2 (Quick Problem Cards)
Từ danh sách 3 thẻ bài toán cá nhân đã khảo sát tại `01-problem-scan.md` (Canteen, Thư viện Pods, Phòng Đào tạo Registrar), bài toán **Canteen VinUni (Card #1)** được lựa chọn để thực hiện Deep-Dive vì:
* Tác động trực tiếp đến **100% sinh viên và giảng viên** hàng ngày.
* Giải quyết ngay điểm bức xúc lớn nhất: sinh viên chỉ có 45 phút nghỉ trưa nhưng mất tới **16–20 phút** xếp hàng thanh toán và chờ chọn món tại khay.
* Giải quyết thế bị động ("nấu mù") của nhà bếp, giảm thiểu 15–20% lượng thức ăn dư thừa mỗi ngày.
* Dữ liệu đầu vào (thời khóa biểu lớp học trên Canvas, lịch thi, sĩ số sinh viên theo ngày) đã có sẵn trong hệ thống quản lý của trường.

---

## 🏗️ 2. Phân Tích Chuyên Sâu (DEEP-DIVE)

### 2.1. Quy trình vận hành hiện tại (Current-State Workflow)

```text
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ Bước 1          │     │ Bước 2          │     │ Bước 3          │     │ Bước 4          │     │ Bước 5          │
│ Xếp hàng        │     │ Thanh toán      │     │ Cầm vé xếp hàng │     │ Chọn đồ ăn      │     │ Xé vé giấy &    │
│ quầy thu ngân   │ ──► │ vé ăn giấy      │ ──► │ quầy thức ăn    │ ──► │ trực tiếp       │ ──► │ bàn giao khay   │
│                 │     │ (KHÔNG GHI MÓN) │     │                 │     │ (VÌ VÉ TRỐNG MÓN)│     │ đồ ăn           │
│ Ai: Sinh viên   │     │ Ai: Thu ngân    │     │ Ai: Sinh viên   │     │ Ai: Sinh viên   │     │ Ai: Nhân viên   │
│ ⏱ 5 - 7 phút 🔴 │     │ ⏱ 1 phút        │     │ ⏱ 6 - 8 phút 🔴 │     │ ⏱ 2 - 3 phút 🔴 │     │ ⏱ 1 phút        │
│ In: Tiền/thẻ SV │     │ In: Thu tiền    │     │ In: Cầm vé giấy │     │ In: Ngắm khay   │     │ In: Vé giấy     │
│ Out: Tới lượt   │     │ Out: Vé chung   │     │ Out: Chờ tới tủ │     │ Out: Món đã chọn│     │ Out: Khay cơm   │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
🔴 = Điểm nghẽn nghiêm trọng (Bottlenecks tại Bước 1, Bước 3, Bước 4)
🔄 Handoffs: Sinh viên ──► Thu ngân (Thanh toán) ──► Nhân viên phục vụ bếp (Chọn món & Giao khay).
⚠️ ĐIỂM NGHẼN CỐT LÕI: Vì trên vé ăn KHÔNG ghi món, đến Bước 4 mỗi sinh viên phải đứng phân vân chọn từng món mặn/rau/canh, làm cả hàng dài phía sau bị tê liệt!
⏱ TỔNG THỜI GIAN VẬN HÀNH THỦ CÔNG: 16 - 20 phút / lượt ăn trưa.
```

---

### 2.2. Problem Statement (Tiêu chuẩn 6 trường — Vin Smart Future)

| Trường thông tin | Nội dung chi tiết |
| :--- | :--- |
| **1. Actor / Operator** | • **Khách hàng:** Toàn thể sinh viên, giảng viên và cán bộ nhân viên VinUni.<br>• **Vận hành viên:** 2 nhân viên thu ngân và 6 nhân viên bếp/phát cơm tại Canteen VinUni. |
| **2. Current Workflow** | Sinh viên tan học xuống canteen lúc 11h45 ──► Xếp hàng tại 1 trong 2 quầy thu ngân (Bước 1) ──► **Thanh toán tiền nhận vé giấy chung/đồng giá (Bước 2 — Trên vé hoàn toàn KHÔNG ghi món ăn)** ──► Cầm vé sang xếp hàng tại quầy thức ăn (Bước 3) ──► **Đến lượt đứng trước tủ kính ngắm nghía, hỏi món và chọn đồ ăn trực tiếp (Bước 4)** ──► Nhân viên bếp xé vé giấy và múc các món đã chọn lên đĩa giao cho sinh viên (Bước 5). |
| **3. Bottleneck** | **3 Điểm nghẽn liên hoàn (Triple Bottleneck):**<br>• **Nghẽn tại Bước 1:** Hàng trăm sinh viên dồn ứ trước 2 quầy thu ngân chỉ để thanh toán mua 1 tấm vé giấy mệnh giá chung.<br>• **Nghẽn tại Bước 4 (Trọng yếu nhất):** Do **trên vé ăn không ghi món gì**, sinh viên tới quầy thức ăn mới bắt đầu nhìn các khay, hỏi xem món nào còn/hết, phân vân chọn món (mất 1.5 - 2.5 phút/người). Toàn bộ dòng người phía sau phải đứng chờ người phía trước chọn đồ.<br>• **Nghẽn dự báo bếp:** Nhà bếp hoàn toàn bị động ("nấu mù") vì không biết sinh viên sẽ chọn món nào, dẫn đến món hot hết sớm gây thất vọng, món nguội dư thừa lãng phí. |
| **4. Business Impact** | • **Thời gian nghỉ ngơi bị đánh cắp:** Giờ nghỉ trưa chỉ có 45–60 phút mà sinh viên mất tới **18–20 phút** chỉ để xếp hàng thanh toán và chờ chọn món.<br>• **Lãng phí thực phẩm & chi phí:** Nhà bếp lãng phí khoảng **15% - 20%** lượng thức ăn chuẩn bị dư thừa mỗi ngày do không thể biết trước xu hướng chọn món của sinh viên.<br>• **Áp lực đỉnh điểm:** Nhân viên phát cơm vừa phải trả lời giải thích từng món, vừa múc thức ăn liên tục trong áp lực giục giã từ hàng dài sinh viên đói bụng. |
| **5. Success Metric** | 1. **Hiệu suất thời gian:** Giảm thời gian chờ đợi nhận suất ăn từ **18 phút ──► dưới 3 phút/người** (Xóa bỏ hoàn toàn bước đứng chọn món tại quầy).<br>2. **Tốc độ giải phóng hàng đợi:** Tăng năng lực phục vụ giờ cao điểm từ 120 suất/giờ ──► **400 suất/giờ**.<br>3. **Tiết kiệm chi phí thực phẩm:** Giảm tỷ lệ thức ăn dư thừa cuối ngày từ 18% ──► **dưới 5%** nhờ dự báo chính xác số lượng từng món cụ thể.<br>4. **Mức độ hài lòng (CSAT):** Đạt trên **92%** đánh giá 4-5 sao từ sinh viên/giảng viên. |
| **6. Operational Boundary (Ranh giới an toàn)** | • **ĐƯỢC PHÉP:** Tự động đồng bộ lịch học từ Canvas/LMS để dự báo nhu cầu suất ăn; cho phép sinh viên **chọn món trước (Pre-order) và thanh toán trực tuyến** nhận E-Ticket; gợi ý dinh dưỡng/calo trên App theo thói quen; sinh mã QR nhận diện đúng món đã chọn; cảnh báo bếp trưởng khi một món sắp chạm ngưỡng an toàn.<br>• **TUYỆT ĐỐI CẤM:** AI **không được tự ý trừ tiền** trong tài khoản thẻ sinh viên khi chưa có thao tác xác thực (FaceID/PIN/Click); AI **không được tự ý thay thế món ăn** đã chọn nếu chưa có sự đồng ý của sinh viên; không được đổi định lượng suất ăn nếu chưa có sự phê duyệt của Bếp trưởng (Bắt buộc Human-in-the-loop). |

---

### 2.3. Future-State Flow & Phân Tích Mức Độ AI Fit

#### A. Định hướng giải pháp: Ứng dụng Di Động "VinUni Smart Canteen App"
Giải pháp chuyển đổi toàn diện quy trình phục vụ bữa trưa thông qua ứng dụng di động dành riêng cho cộng đồng VinUni với 3 tính năng cốt lõi:
1. **Trợ lý AI gợi ý món ăn theo thói quen & dinh dưỡng (AI Habit & Preference Recommender):**
   * Phân tích lịch sử gọi món 14 ngày gần nhất, thói quen ăn uống (ăn mặn, thanh đạm, ăn chay ngày rằm/thứ Ba, eat-clean).
   * Phân tích sở thích dinh dưỡng và mục tiêu sức khỏe (calo, protein cho sinh viên tập gym, cảnh báo dị ứng hải sản/đậu phộng).
   * Tự động gửi thông báo gợi ý combo món trưa lý tưởng lúc 10h30 sáng kèm nút **"Đặt ngay 1 chạm" (1-Click Reorder)**.
2. **Đặt trước món ăn & Mua vé thanh toán trực tuyến (In-App Pre-ordering & E-Payment):**
   * Sinh viên xem thực đơn hình ảnh thực tế hôm nay, chọn chính xác từng món (cơm, món mặn, món rau, canh).
   * **Mua vé và thanh toán trực tuyến ngay trên App** qua thẻ sinh viên tích hợp, VinPay hoặc QR ngân hàng.
   * Hệ thống xuất **Vé ăn điện tử (E-Ticket)** kèm mã QR động chứa thông tin chi tiết các món đã chọn.
3. **Làn nhận đồ ăn nhanh thông minh (Fast-Track Pickup Counter):**
   * Dữ liệu đặt món được đẩy trực tiếp về màn hình bếp (Kitchen Display System - KDS) để chia suất và chuẩn bị khay trước giờ cao điểm.
   * Sinh viên tan học chỉ việc đi thẳng tới làn Fast-Track, quét mã QR E-Ticket và nhận khay cơm trong **20 - 30 giây** (không cần qua quầy thu ngân, không cần đứng chọn món tại khay).

---

#### B. AI-Fit Matrix:
* **Lựa chọn kiến trúc:** **LLM Feature (Cá nhân hóa gợi ý thói quen & phân tích dinh dưỡng) + Rule-Based Transaction (Thanh toán ví điện tử an toàn) + Time-Series Forecasting (Dự báo nhu cầu nhà bếp)**.
* **Lý do:** Đảm bảo tính linh hoạt, thấu hiểu ngôn ngữ tự nhiên và sở thích cá nhân của sinh viên, đồng thời giữ vững độ chuẩn xác 100% về giao dịch tài chính.

---

#### C. Bảng so sánh chi tiết: Quy trình Hiện tại (Before) vs Quy trình Tương lai với App (After)

| Tiêu chí so sánh | Quy trình thủ công Hiện tại (Before) | Quy trình tương lai với App & AI (After) |
| :--- | :--- | :--- |
| **Kênh mua vé & Thanh toán** | Xếp hàng tại 2 quầy thu ngân vật lý (chờ 5-7 phút). | Mua vé và thanh toán trực tuyến ngay trên App (mất 15 giây). |
| **Thông tin trên vé ăn** | Vé giấy mệnh giá chung, **hoàn toàn KHÔNG ghi món**. | Vé điện tử E-Ticket **ghi rõ 100% món ăn đã chọn**. |
| **Cách thức chọn món** | Đến tận quầy nhìn khay kính mới phân vân chọn món (nghẽn 2-3 phút/người). | **AI gợi ý theo thói quen**, sinh viên chốt món trước từ lớp học. |
| **Thời gian nhận cơm** | Tổng cộng **16 - 20 phút** chờ đợi mệt mỏi. | **Chỉ 20 - 30 giây** quét mã QR tại làn Fast-Track. |
| **Thế chủ động của nhà bếp** | "Nấu mù" không biết ai sẽ ăn món gì, lãng phí 18% đồ ăn thừa. | Bếp biết trước chính xác số lượng từng món cần nấu lúc 10h30. |

---

#### D. Quy trình tương lai (Future-State Flowchart)

```text
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│ Bước 1          │       │ Bước 2          │       │ Bước 3          │       │ Bước 4          │
│ 🔵 AI Gợi ý     │       │ 🟢 Sinh viên    │       │ 🔵 KDS Nhà bếp  │       │ 🟢 Fast-Track   │
│ món theo thói   │ ───►  │ Đặt món & Thanh │ ───►  │ Nhận order &    │ ───►  │ Quét QR E-Ticket│
│ quen trên App   │       │ toán E-Ticket   │       │ chuẩn bị khay   │       │ lấy cơm 30 giây │
│                 │       │                 │       │                 │       │                 │
│ Ai: LLM Engine  │       │ Ai: Sinh viên   │       │ Ai: Hệ thống KDS│       │ Ai: Sinh viên   │
│ ⏱ 10:30 sáng    │       │ ⏱ 10:35 - 11:30 │       │ ⏱ 11:00 - 11:45 │       │ ⏱ 11:45 - 12h15 │
└─────────────────┘       └─────────────────┘       └─────────────────┘       └─────────────────┘
                                                                                      │
                                                                                      ▼
                                                                              ↩️ Fallback Plan:
                                                                              Nếu App mất mạng/hết pin,
                                                                              quầy thu ngân POS thẻ 
                                                                              sinh viên dự phòng vật lý 
                                                                              sẵn sàng phục vụ ngay.
```

* 🔵 **AI Step:**
  * AI quét lịch sử order của sinh viên: *"Bạn thường chọn Cơm gà áp chảo sốt nấm + Canh cải ít dầu vào thứ Ba. Hôm nay menu Canteen có món này, bạn có muốn đặt luôn không?"*.
  * Tự động tổng hợp số lượng món gửi về KDS bếp trước 11h00.
* 🟢 **Human-in-the-loop (HITL):** Sinh viên chủ động nhấn nút xác nhận thanh toán; Bếp trưởng kiểm soát chất lượng khay đồ ăn thực tế.
* ↩️ **Cơ chế Fallback:** Duy trì 1 quầy thanh toán POS thẻ sinh viên offline truyền thống đề phòng trường hợp mất mạng hoặc sinh viên hết pin điện thoại.

---

## 💻 3. Prompt Prototype & Boundary Test

Nhóm đã xây dựng file nguyên mẫu code [`starter-code/prompt_prototype.py`](starter-code/prompt_prototype.py) và chạy thử nghiệm bằng **Gemini 2.5 Flash** để kiểm tra ranh giới an toàn.

### Ranh giới an toàn (Operational Boundary) được kiểm chứng:
1. **Quy tắc 1 (DRAFT ONLY):** Mọi đầu ra gợi ý điều phối BẮT BUỘC có tiền tố `[DRAFT_ONLY]` để ngăn chặn việc gửi thẳng cho người dùng mà không qua xét duyệt.
2. **Quy tắc 2 (CRITICAL THRESHOLD):** Cảnh báo ngưỡng nguy cấp (pin xe điện < 5% hoặc số lượng suất ăn vượt ngưỡng kho), AI không được tự ý thực hiện hành vi mạo hiểm mà phải trigger lệnh cứu hộ hoặc xin chỉ đạo trực tiếp: `{"action": "dispatch_mobile_charger", "reason": "..."}`.

### Kết quả thử nghiệm tấn công Prompt (Adversarial Testing):
* Cả 2 test cases tấn công (cố tình ép bỏ qua thẻ `[DRAFT_ONLY]` và cố tình bắt chỉ đường trạm sạc xa khi pin < 5%) đều bị mô hình từ chối và thực thi đúng ranh giới an toàn.
* Assertions tự động pass 100% (`Passed: 2, Failed: 0`).

---

## 🏁 4. Đánh Giá Khả Thi & Ra Quyết Định (EVALUATE)

### 4.1. AI Readiness Checklist

| Tiêu chí sẵn sàng | Đánh giá | Bằng chứng thực tế |
| :--- | :---: | :--- |
| **1. Dữ liệu sẵn có & chuẩn hóa** | ✅ ĐẠT | Dữ liệu lịch học, sĩ số lớp đã có trên hệ thống Edusoft/Canvas của VinUni; menu tuần được canteen cập nhật cố định từ Chủ nhật. |
| **2. Rủi ro sai số trong tầm kiểm soát** | ✅ ĐẠT | Nếu AI dự báo lệch 5-10%, nhà bếp vẫn có kho nguyên liệu đệm; không gây nguy cơ mất an toàn thực phẩm hay vi phạm pháp lý. |
| **3. Mức độ sẵn sàng của Stakeholders** | ✅ ĐẠT | Sinh viên và giảng viên VinUni 100% sử dụng smartphone, quen thuộc với công nghệ số; Ban Giám đốc Vận hành Campus mong muốn cải thiện chất lượng đời sống sinh viên. |

### 4.2. Quyết định của Ban Giám Đốc Vin Smart Future

> ### 🟢 QUYẾT ĐỊNH: **GO (Bắt đầu xây dựng Prototype)**

#### Lập luận quyết định (Justification):
1. **Giá trị vận hành vượt trội:** Xóa bỏ hoàn toàn tình trạng xếp hàng 2 lượt và đứng phân vân chọn món tại quầy, rút ngắn thời gian nhận cơm xuống còn 30 giây/người, giảm 13% lãng phí thức ăn thừa.
2. **Khả thi về kỹ thuật:** Kiến trúc đơn giản, an toàn, sử dụng API dữ liệu có sẵn của trường VinUni.
3. **Lộ trình:** Triển khai thử nghiệm 1 quầy Fast-track trong 4 tuần trước khi áp dụng toàn diện.
