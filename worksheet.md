# Worksheet — Tô Bài (AI Notes cho học viên khoá học online)

Họ tên: Lê Thị Châm Anh · MSSV: 2A202602846 · Ngày làm: 10/10/2026

> **Sản phẩm:** học viên tô xanh/đỏ trên tài liệu bài học ngay trong LMS → AI viết bản note ôn tập cá nhân (trọng tâm + giải đáp đoạn tô đỏ + tự kiểm tra, tối đa 2 lượt "Hỏi tiếp").
> **Giá:** $0,25 / bài học được giải quyết xong, trần $2/học viên/tháng. Trung tâm đào tạo trả tiền, học viên không trả.
> **Nguồn số:** mọi ô `x!Bn` dưới đây là ô trong `LeThiChamAnh_Day22_model.xlsx` (repo Day 22).
> **Hiện trạng thật tại 10/10/2026:** chưa nói chuyện với partner, chưa có học viên thật, mới có 1 phiên thử (05/10/2026). Mọi "số hiện tại" bên dưới là **số mô hình** hoặc **chưa có**, không phải số đo.

---

## Trạm 1 — Loại mô hình

**3 câu hỏi (theo thực tế hôm nay):**

| Câu hỏi | Trả lời |
|---|---|
| Ai trả tiền? | **Doanh nghiệp**: trung tâm đào tạo (partner mục tiêu: Chương trình A.I Thực Chiến – VinUniversity), từ ngân sách *vận hành đào tạo* (giờ trợ giảng/mentor). Học viên không trả. |
| Ai dùng? | **Học viên của trung tâm**, không phải người ký hợp đồng → khách hàng *của* người trả tiền. |
| Có chạm end-user không? | **Có.** Nút "Tô Bài" mang tên mình nằm trong trang "Nội dung bài học" của LMS; học viên thao tác trực tiếp, mình giữ log từng job theo `user_id` (lưu / bỏ / hỏi trợ giảng). |

**Câu chốt loại:** Chúng tôi là **B2B2C (biến thể embedded có thương hiệu)** vì tiền đến từ **trung tâm đào tạo** (ngân sách giờ trợ giảng), người dùng thật là **học viên của trung tâm**, và chúng tôi chạm được họ qua **nút "Tô Bài" trong trang "Nội dung bài học" của LMS A.I Thực Chiến**, có log từng học viên.

*Vì sao không phải B2B:* người dùng không phải người trả tiền, và mình có dữ liệu + thương hiệu trước mặt học viên. *Vì sao không phải B2C:* học viên không trả đồng nào. → **Đèn bật trước: partner activation** — trung tâm ký rồi mà không bật Tô Bài cho học viên thì doanh thu = 0 dù "đã có partner".

**3 biến B2B2C áp vào Tô Bài:**
- *Rủi ro inference bất đối xứng:* partner quyết định volume (bật mặc định trên mọi bài lab, dồn deadline) nhưng **mình trả token cho mọi lần thử**, còn chỉ được tính tiền khi job *xong* (lưu + không hỏi trợ giảng 72h) và *dưới trần 8 bài/HV/tháng*. Job thất bại và job vượt trần = chi phí không có doanh thu.
- *Tranh chấp attribution:* "học viên hiểu bài" là công của mentor hay của Tô Bài? Không chốt được → đó là lý do Day 22 chọn **Usage**, không chọn Outcome.
- *GM sau rev-share:* hợp đồng trực tiếp với trung tâm → rev-share = 0% hôm nay; nếu tháng 4+ đi qua đơn vị phân phối plugin Moodle thì phải trừ.

**Bảng đèn §3.3 B2B2C** (đủ 9 dòng + 1 đèn riêng của sản phẩm):

| # | Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|---|
| 1 | Partner activation rate ⭐ | 🔧 | Chưa có partner go-live. Cần: bảng partner + ngày go-live, log job có `user_id` và cờ `is_test` (loại tài khoản mentor/của tôi). Số đầu tiên: 1 tuần sau pilot (~02/11/2026). |
| 2 | End-user reach trong partner | 🔧 | Tử số có từ log. **Mẫu số** (sĩ số cohort) phải xin partner — ghi thành 1 dòng trong email đồng ý pilot. |
| 3 | Time-to-first-end-user | 🔧 | Cần ngày partner đồng ý pilot (email) + timestamp job đầu tiên của học viên thật. Có ngay khi pilot chạy. |
| 4 | Volume volatility | 🔧 | Log job/ngày làm trong 2 tuần, nhưng cần ≥3 tháng volume mới có độ lệch chuẩn có nghĩa → số đầu tiên ~01/2027. |
| 5 | GM sau rev-share | 🔧 | Hôm nay chỉ có số mô hình 71,1% (`2_Pricing!B21`). Cần: usage log token thật/job + đối chiếu hoá đơn API tháng. Rev-share = 0%. |
| 6 | Chi phí inference ÷ doanh thu — theo partner | 🔧 | Mô hình: 22,2% (tính ở [MH] 2). Cần gắn `partner_id` vào metadata mỗi API call. |
| 7 | Tập trung volume | ✅ | Đo được ngay nhưng = 100% theo thiết kế (90 ngày đầu chỉ 1 partner). Rủi ro đã chấp nhận; chỉ có nghĩa từ tháng 4+. |
| 8 | Chất lượng nhìn từ end-user | ❌ | Chưa có bộ eval, chưa có SLA, chưa có định nghĩa "giải thích đúng" được partner đồng ý (Attribution 3/10, `3_Value_Metric!B10`). Bộ eval 30 bài: hạn 23/10/2026. |
| 9 | Doanh thu/partner · partner NRR · GM tổng | ❌ | Chưa có khách trả tiền. Doanh thu từ cohort trả tiền (tháng 2–3); NRR cần ≥12 tháng. |
| + | **Containment rate** (đèn riêng) | ❌ → 🔧 | 75% là **ước tính thô** (`1_Cost_Job!B10`), chưa đo. Log 3 trạng thái lưu/bỏ/hỏi trợ giảng làm trong 2 tuần. |

---

## Trạm 2 — Thẻ đèn

**North Star:** **Số bài học được giải quyết xong / tuần** (= đơn vị tính tiền = giá trị học viên nhận) — hiện tại **0** (chưa có học viên thật) — mục tiêu **≥ 42/tuần trong pilot 40 HV**, **≥ 156/tuần khi cohort trả tiền 150 HV**.
*(42 = 40 HV × 75% reach × 6 bài ÷ 4,33 tuần; 156 = 150 × 75% × 6 ÷ 4,33 — ngưỡng reach 75% xem [MH] 3.)*
*Vì sao không chọn partner activation làm North Star:* 90 ngày đầu chỉ có 1 partner → đèn đó là 0/1, không đổi theo tuần. North Star này là tích của cả 3 phễu: partner đẩy × học viên dùng × AI làm xong.

| # | Tầng | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **Partner activation rate** ⭐ | Partner đã go-live (Tô Bài bật trên ≥1 bài lab) có ≥1 job **hoàn thành** của học viên thật trong 30 ngày. **Không** tính: tài khoản mentor, admin, tài khoản của tôi, job lúc demo. | Partner go-live có ≥1 job hoàn thành của HV thật ÷ partner đã go-live | Tuần · Châm Anh, từ log | → #3 reach → #8 doanh thu/partner |
| 2 | L | **Time-to-first-end-user (TTFEU)** | Số ngày lịch từ ngày partner **đồng ý pilot bằng văn bản** (email) đến job hoàn thành đầu tiên của học viên thật. **Không** tính job test, job do tôi/mentor tạo. | Ngày(job thật đầu tiên) − Ngày(email đồng ý) | Mỗi partner · Châm Anh | → #1 activation → cổng ngày 30 (đủ job để đo containment) |
| 3 | L | **End-user reach** | % học viên **có tên trong danh sách cohort** đã có ≥1 job hoàn thành trong 14 ngày đầu cohort. **Không** tính học viên chỉ mở nút rồi bỏ, không tính người ngoài danh sách. | HV có ≥1 job hoàn thành ÷ sĩ số cohort (partner cung cấp) | Tuần · Châm Anh | → North Star → #8 MRR/HV → CAC payback |
| 4 | O | **Containment rate** | Job thử kết thúc bằng: HV **LƯU** note **và** không bấm "Hỏi trợ giảng" cho bài đó trong 72h. **Không** tính vào tử: bản bị bỏ, tạo lại, lỗi, đã chuyển trợ giảng. Mẫu số: **mọi** job thử (kể cả lỗi). | Job hoàn thành ÷ job thử (cửa sổ cuộn 200 job, trễ 72h) | Tuần · Châm Anh | → #5 inference/doanh thu → #7 GM |
| 5 | O | **Chi phí inference ÷ doanh thu — theo partner** 💲 | Toàn bộ tiền LLM + infra + retry của **mọi** job thử (kể cả job thất bại và job vượt trần 8 bài/HV) của partner đó ÷ doanh thu đã tính tiền của partner đó. **Không** lấy trung bình mọi partner; **không** gồm QA nội bộ. | Σ chi phí API thật (theo `partner_id`) ÷ (job tính tiền × $0,25) | Tuần · Châm Anh, từ usage log API | → #7 GM sau rev-share (bắt chi phí trước khi GM tháng ra số) |
| 6 | O | **Chất lượng nhìn từ end-user** | % đoạn tô đỏ AI giải thích **đúng** trên bộ eval cố định (30 bài lab × 3 đoạn = 90 mẫu, chấm theo đáp án mentor). **Không** chấm văn phong, chỉ chấm đúng/sai kiến thức. Cộng thêm: số lỗi sai kiến thức partner phải đính chính với lớp. | Mẫu chấm đúng ÷ 90 | Mỗi lần đổi prompt/model + 2 tuần/lần · Châm Anh chấm, 1 mentor kiểm 10 mẫu | → #4 containment (HV gặp note sai sẽ hỏi trợ giảng) → partner gỡ Tô Bài (#1) |
| 7 | O | **GM sau rev-share — theo partner** | Doanh thu đã tính tiền − rev-share − COGS thật (API + infra + retry + QA nội bộ). **Không** gồm R&D, công sales. | (Doanh thu − rev-share − COGS) ÷ doanh thu | Tháng · Châm Anh | → #8 doanh thu/partner có lãi không → quyết định cổng 90 |
| 8 | G | **Doanh thu tính tiền / học viên / tháng (MRR/HV)** | Hoá đơn tháng gửi partner ÷ sĩ số cohort. **Không** tính tháng pilot miễn phí. | MRR partner ÷ sĩ số cohort | Tháng (đọc theo quý) · Châm Anh | Bảng điểm: CAC payback, LTV/CAC |

**Đếm:** 3 Leading · 4 Operating · 1 Lagging (12,5% lagging). **Đèn chi phí AI là đèn số: 5** (và #4, vì containment quyết định Cost/Job thật — xem [MH] 1).

---

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | Partner activation rate ⭐ | ≥ 60% | 30–60% | < 30% (với n=1: không có HV thật sau 30 ngày go-live) | [TB] | Không có benchmark công bố theo loại mô hình (HANDBOOK §2.8 ①) → dùng mốc HANDBOOK §3.3 làm điểm xuất phát, đặt lại sau 2 đợt partner (tháng 4+, 3–5 partner); 90 ngày đầu đèn này nhị phân nên #2 gánh thay. |
| 2 | Time-to-first-end-user | ≤ 7 ngày | 8–14 ngày | > 14 ngày | [MH] | Cổng ngày 30 cần ≥ 60 job thử; pilot 40 HV sinh ~8 job thử/ngày → cần 7,5 ngày dùng thật trước 09/11 → xem [MH] 4. |
| 3 | End-user reach (14 ngày) | ≥ 75% | 50–75% | < 50% | [MH] | 75% là mức tối thiểu để MRR $225 (KPI tháng 2–3 Day 22) còn đạt được ngay cả khi mọi HV dùng chạm trần 8 bài; < 50% thì CAC tối đa < $960, tức payback của ngân sách CAC Day 22 dài gấp đôi giới hạn 12 tháng → [MH] 3. |
| 4 | Containment rate | ≥ 54,2% | 43,4–54,1% | < 43,4% | [MH] | 54,1% là breakeven để GM ≥ 60% (`2_Pricing!B33`), 43,3% là điểm GM rơi xuống 50% — số tính ra, không tròn → [MH] 1. |
| 5 | Inference ÷ doanh thu (theo partner) | ≤ 30,7% | 30,8–38,4% | > 38,5% | [MH] | QA nội bộ ăn thêm 30% so với chi phí inference, nên inference vượt 30,7% doanh thu là GM tụt dưới 60%, vượt 38,5% là dưới 50% → [MH] 2. |
| 6 | Chất lượng (eval 90 mẫu) | ≥ baseline đợt 1 | thấp hơn baseline 1–5 điểm % | thấp hơn > 5 điểm %, **hoặc** ≥ 1 lỗi kiến thức partner phải đính chính với lớp | [TB] | Chưa có eval và chưa có SLA → đo đợt 1 (23/10/2026) + đợt 2 (06/11/2026) làm baseline; 5 điểm % ≈ 5/90 mẫu, dưới mức đó có thể là nhiễu chấm; lỗi bị partner đính chính là đỏ ngay vì Tô Bài nằm trong thương hiệu của partner (bài học Klarna). |
| 7 | GM sau rev-share | ≥ 60% | 50–60% | < 50% | [MH] + [BM] neo | 60% là GM mục tiêu (`2_Pricing!B32`), 50% là mốc "mô hình gãy" Day 22; neo [BM]: GM AI-native ~53% năm 2026P (ICONIQ *State of AI 2026*, 07/2026 — kiểm tra 27/08/2026 qua HANDBOOK §8 mục 7) → 🟡 nằm quanh trung vị ngành, không phải mục tiêu. |
| 8 | MRR / học viên / tháng | ≥ $1,125 | $0,75–1,124 | < $0,75 | [MH] | = reach 75% / 50% × 6 bài × $0,25; với cohort 150 HV là $168,75 / $112,5 → [MH] 3. |

> **Benchmark không dùng nhưng đã cân nhắc:** NRR trung vị SaaS 101% (Benchmarkit 2025, dữ liệu FY2024 — qua HANDBOOK §8 mục 10, chốt 27/08/2026). Chưa đưa vào dashboard vì NRR cần ≥12 tháng dữ liệu → ghi ở mục "Chưa đo được".

### Phụ lục [MH] — phép tính

**[MH] 1 — Containment rate**

```
Đầu vào (Day 22 model):
  P  = giá / job hoàn thành                 = $0,25        (2_Pricing!B19)
  v  = chi phí biến đổi / job THỬ           = $0,041644    (2_Pricing!B29 = LLM 0,0293 + infra 0,01 + retry 0,002344)
  q  = QA nội bộ / job thử                  = $0,0125      (2_Pricing!B30 = 5% × 3 phút/60 × $5/giờ)
  e  = escalate                             = 0            (Biến thể A — trung tâm tự xử lý, 1_Cost_Job!B6)
Phép tính:
  Cost / job hoàn thành = (v + q) / R = 0,054144 / R
  GM(R) = 1 − 0,054144 / (0,25 × R) = 1 − 0,216576 / R
  GM = 60%  →  R = 0,216576 / 0,40 = 54,14%     (khớp 2_Pricing!B33)
  GM = 50%  →  R = 0,216576 / 0,50 = 43,32%
  Kiểm tra: R = 75% (ước tính) → GM = 1 − 0,2888 = 71,1%  (khớp 2_Pricing!B21)
Kết quả → 🟢 ≥ 54,2% · 🟡 43,4–54,1% · 🔴 < 43,4%
```

**[MH] 2 — Chi phí inference ÷ doanh thu (đèn chi phí AI)**

```
Đầu vào: v = $0,041644 / job thử · q = $0,0125 / job thử · P = $0,25 · R = containment
Phép tính:
  Inference share  s  = v / (P × R)
  COGS share          = (v + q) / (P × R) = s × (1 + q/v) = s × 1,30   (q/v = 0,0125/0,041644 = 0,300)
  GM ≥ 60%  ⇔  1,30 × s ≤ 0,40  ⇔  s ≤ 30,77%
  GM ≥ 50%  ⇔  1,30 × s ≤ 0,50  ⇔  s ≤ 38,46%
  Mô hình hôm nay (R = 75%): s = 0,041644 / 0,1875 = 22,2%  → 🟢 trên giấy
Vì sao cần đèn này dù đã có containment: nó bắt thêm 2 thứ containment không thấy —
  (a) token/job thật cao hơn 3 lượt × 8.700 token giả định (1_Cost_Job!B19:B22),
  (b) job VƯỢT TRẦN 8 bài/HV/tháng: tốn token nhưng không được tính tiền.
Kết quả → 🟢 ≤ 30,7% · 🟡 30,8–38,4% · 🔴 > 38,5%
```

**[MH] 3 — End-user reach và MRR / học viên**

```
Đầu vào: cohort trả tiền 150 HV (5_90Day_Plan!C13) · 6 bài hoàn thành / HV dùng / tháng (one-pager Day 22)
         trần 8 bài / HV / tháng · P = $0,25 · GM = 71,1% (2_Pricing!B21) · payback tối đa 12 tháng (SMB, 4_Channel_Fit!B8)
Phát hiện: ARPU $225 của Day 22 (4_Channel_Fit!B5) = 150 × 6 × 0,25 → ngầm giả định 100% HV đều dùng.
Phép tính:
  MRR(reach r) = 150 × r × 6 × 0,25 = 225 × r
  CAC tối đa  = MRR × GM × 12        = 1.920 × r
  Muốn MRR ≥ $225 khi mọi HV dùng chạm trần: 150 × r × 8 × 0,25 ≥ 225 → r ≥ 75%
  r = 75%: MRR = $168,75 · CAC tối đa = $1.440 · MRR/HV = $1,125
  r = 50%: MRR = $112,50 · CAC tối đa = $960   · MRR/HV = $0,75
           nếu vẫn tiêu đủ ngân sách CAC Day 22 ($1.920) → payback = 1.920 / (112,5 × 0,711) = 24 tháng = 2× giới hạn SMB
Kết quả (reach)  → 🟢 ≥ 75% · 🟡 50–75% · 🔴 < 50%
Kết quả (MRR/HV) → 🟢 ≥ $1,125 · 🟡 $0,75–1,124 · 🔴 < $0,75
```

**[MH] 4 — Time-to-first-end-user**

```
Đầu vào: pilot 40 HV (giữa 30–50, 5_90Day_Plan!B13) · bắt đầu ~26/10/2026 · cổng ngày 30 = 09/11/2026
         reach mục tiêu 75% · 6 bài hoàn thành / HV / tháng · containment 75%
Phép tính:
  Job thử / ngày = 40 × 75% × 6 / 75% / 30 = 8 job thử / ngày
  Cổng 30 cần ≥ 60 job thử (khoảng tin cậy 95% của containment ≈ ±12,7 điểm %, đủ phân biệt 75% với breakeven 54%)
  → cần 60 / 8 = 7,5 ngày học viên dùng thật trước 09/11
  → job thật đầu tiên phải có trước ~01/11 = tối đa ~7 ngày sau ngày bắt đầu pilot
  > 14 ngày (sau 09/11): cổng 30 chắc chắn trượt, Pilot Report 20/11 có < 2 tuần dữ liệu
Kết quả → 🟢 ≤ 7 ngày · 🟡 8–14 ngày · 🔴 > 14 ngày
```

**[MH] 5 — GM sau rev-share: được nhường tối đa bao nhiêu % cho bên phân phối?**

```
Đầu vào: GM trước rev-share = 71,1% (R = 75%) · GM mục tiêu 60%
Phép tính: rev-share tối đa = 71,1% − 60% = 11,1% doanh thu (khi containment đúng 75%)
           nếu containment thật chỉ 60% → GM = 1 − 0,216576/0,60 = 63,9% → rev-share tối đa 3,9%
Dùng khi: tháng 4+ đàm phán phân phối plugin Moodle — không ký rev-share > 11% khi chưa có containment đo được.
Kết quả → 🟢 ≥ 60% · 🟡 50–60% · 🔴 < 50%
```

---

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (có 3).

1. ⏹ **NẾU** time-to-first-end-user > 14 ngày **TRÊN** partner pilot hiện tại (A.I Thực Chiến) **THÌ** dừng mọi việc tìm partner thứ hai và dừng đóng gói plugin Moodle trong 2 tuần; tuần đó xin ban vận hành bật Tô Bài **mặc định** trên đúng 1 bài lab sắp đến hạn và vào lớp demo 10 phút. **KHÔNG THÌ** không được đi ký/chào thêm trung tâm khác để bù — một partner không đẩy cộng thêm một partner không đẩy vẫn là 0 học viên.

2. ⏹ **NẾU** end-user reach < 50% **TRONG** 14 ngày đầu của cohort **VÀ** cohort có ≥ 30 học viên trong danh sách **THÌ** đóng băng mọi tính năng mới trong 2 tuần; làm đúng 2 việc: (a) gửi partner danh sách bài lab chưa bật Tô Bài, (b) phỏng vấn 5 học viên *chưa dùng* xem họ có thấy nút không. **KHÔNG THÌ** không làm thêm tính năng partner/học viên đòi (export, flashcard…) — người không thấy nút thì tính năng mới cũng không thấy.

3. ⏹ **NẾU** containment < 43,4% **TRÊN** 200 job thử gần nhất **VÀ** ≥ 30 học viên khác nhau tạo ra số job đó **THÌ** dừng bật tính tiền $0,25/bài và không mở thêm lớp; tuần sau đọc toàn bộ job bị chuyển trợ giảng, sửa prompt/tài liệu nguồn cho 3 bài lab có tỉ lệ chuyển cao nhất, chạy lại eval. **KHÔNG THÌ** không được nới định nghĩa "giải quyết xong" (bỏ điều kiện 72h, đếm cả bản chưa lưu) để con số đẹp lên, và không tăng giá/bài để bù biên.

4. **NẾU** chi phí inference ÷ doanh thu > 38,5% **TRONG** 1 tháng **VÀ** partner đó có ≥ 300 job tính tiền trong tháng **THÌ** trong sprint tới: khoá nút Tô Bài khi HV đã đạt trần 8 bài/tháng (hiện thông báo "đã dùng hết lượt tháng này"), và cắt input fresh chỉ còn đoạn tô + 1 trang ngữ cảnh. **KHÔNG THÌ** không nâng trần hoá đơn hay tăng giá đại trà với partner — họ chọn Tô Bài vì hoá đơn ≤ $2/HV, phá trần là mất lý do mua.

5. **NẾU** điểm eval thấp hơn baseline > 5 điểm % **TRÊN** 1 lần chạy eval 90 mẫu, **HOẶC** có ≥ 1 lỗi kiến thức partner phải đính chính với lớp, **THÌ** trong 48 giờ chuyển Tô Bài trên bài lab bị lỗi về chế độ "chỉ bật khi học viên chọn", gửi partner danh sách lỗi + bản sửa, chạy lại eval trước khi bật mặc định lại. **KHÔNG THÌ** không chuyển sang model rẻ hơn (Haiku 5.5 trong kế hoạch tháng 4) hay cắt token để giữ biên trong tuần đó — Tô Bài nằm trong thương hiệu của partner, note sai là khủng hoảng của họ (bài học Klarna).

**Tự kiểm tra:** 5 luật đủ NẾU / TRONG-TRÊN / THÌ / KHÔNG THÌ · luật 2, 3, 4 có vế VÀ vì metric dễ nhiễu khi mẫu nhỏ · 3 luật dừng ⏹ · không luật nào "xem xét lại".

---

## Trạm 5 — nháp cổng gác (bản chính ở `dashboard.md`)

Ngày 0 = 10/10/2026 → ngày 30 = 09/11/2026 · ngày 60 = 09/12/2026 · ngày 90 = 08/01/2027.

| Ngày | Metric (1) | Ngưỡng | Vì sao số này | Bằng chứng vật lý | Nếu trượt |
|---|---|---|---|---|---|
| 30 · cổng **học** | Số job thử của học viên thật có log đủ 3 trạng thái (lưu/bỏ/hỏi trợ giảng) | ≥ 60 job | 60 job → containment đo được với sai số ±12,7 điểm % — đủ biết 75% hay dưới breakeven 54% ([MH] 4) | `pilot_jobs_log.csv` + email partner đồng ý pilot + `eval_round1.md` | Partner không cho pilot trước 23/10 → **PIVOT** kênh (plugin Moodle tự cài cho trung tâm nhỏ — kill-switch Day 22). Có pilot nhưng < 60 job → **FIX** 1 lần: bật mặc định |
| 60 | Containment đo được (trên ≥ 200 job thử) | ≥ 54,2% | Breakeven GM 60% (`2_Pricing!B33`) | Pilot Report (20/11) + log + bảng GM theo partner | 43,4–54,1% → **FIX** 1 lần (prompt/nguồn 3 bài tệ nhất). < 43,4% → **PIVOT**: thu hẹp sang loại bài lab có containment ≥ 54% |
| 90 | Số bài giải quyết xong **và đã tính tiền** trong 30 ngày gần nhất | ≥ 675 bài (= 150 HV × 75% × 6) | Reach 75% ([MH] 3) — MRR ≈ $169 | Hoá đơn gửi partner + log job | 450–674 → **FIX** reach 1 lần. < 450 → **KILL** theo kill criteria |

**Kill criteria:** Dừng Tô Bài nếu **đến 08/01/2027** có **< 450 bài được giải quyết xong và tính tiền trong 30 ngày** (MRR < $112,5 với cohort 150 HV), **hoặc** containment **< 43,4%** trên ≥ 300 job sau khi đã FIX một lần.
