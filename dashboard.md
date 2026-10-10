# OPERATING DASHBOARD — Tô Bài (AI Notes trong LMS)

**Loại mô hình:** B2B2C embedded — trung tâm đào tạo trả $0,25/bài giải quyết xong, học viên dùng nút "Tô Bài" trong LMS · **Cập nhật:** 10/10/2026 · Lê Thị Châm Anh – 2A202602846
**NORTH STAR:** Số bài học được giải quyết xong / tuần — hiện tại **0** (chưa có HV thật) — mục tiêu **≥ 42/tuần** (pilot 40 HV) → **≥ 156/tuần** (cohort trả tiền 150 HV)
*"Hiện" = số mô hình Day 22 hoặc "—" (chưa đo). Pilot dự kiến bắt đầu ~26/10/2026.*

### Đèn báo sớm (Leading — nhìn hằng tuần)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Partner activation ⭐ (≥1 HV thật trong 30 ngày go-live) | 0/0 | ≥60% / 30–60% / <30% | [TB] mốc HANDBOOK, n=1 đến tháng 4 | Reach → MRR/partner |
| Time-to-first-end-user (email đồng ý → job thật đầu tiên) | — | ≤7 / 8–14 / >14 ngày | [MH] 4 | Activation, cổng 30 |
| End-user reach (% sĩ số có ≥1 job xong trong 14 ngày) | — | ≥75% / 50–75% / <50% | [MH] 3 | North Star, MRR/HV |

### Đèn vận hành (Operating — nhìn hằng tuần/tháng)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---|---|---|---|
| Containment (lưu + không hỏi trợ giảng 72h ÷ job thử) | 75% *ước tính thô* | ≥54,2% / 43,4–54,1% / <43,4% | [MH] 1 | Inference/DT, GM |
| 💲 Inference ÷ doanh thu, theo partner (gồm job lỗi + vượt trần) | 22,2% *mô hình* | ≤30,7% / 30,8–38,4% / >38,5% | [MH] 2 | GM sau rev-share |
| Chất lượng: % đúng trên eval 90 mẫu (30 bài × 3 đoạn) | — (eval 23/10) | ≥ baseline / −1–5 điểm / −>5 điểm hoặc 1 lỗi partner phải đính chính | [TB] 2 đợt eval | Containment, partner gỡ Tô Bài |
| GM sau rev-share, theo partner (rev-share = 0%) | 71,1% *mô hình* | ≥60% / 50–60% / <50% | [MH] 1, 5 · [BM] neo AI-native 53% (ICONIQ 07/2026, kiểm tra 27/08/2026 qua HANDBOOK §8) | MRR/partner có lãi |

### Đèn kết quả (Lagging — nhìn hằng quý)

| Đèn | Hiện | 🟢 / 🟡 / 🔴 | Nguồn |
|---|---|---|---|
| MRR / học viên / tháng | $0 (pilot miễn phí) | ≥$1,125 / $0,75–1,124 / <$0,75 | [MH] 3 (= reach × 6 bài × $0,25) |

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ **NẾU** time-to-first-end-user >14 ngày **TRÊN** partner pilot **THÌ** dừng tìm partner 2 và dừng làm plugin Moodle 2 tuần; xin bật Tô Bài mặc định trên 1 bài lab sắp hạn + demo 10' trong lớp. **KHÔNG THÌ** không chào/ký thêm trung tâm để bù.
2. ⏹ **NẾU** reach <50% **TRONG** 14 ngày đầu cohort **VÀ** cohort ≥30 HV **THÌ** đóng băng tính năng mới 2 tuần; gửi partner danh sách bài chưa bật, phỏng vấn 5 HV chưa dùng. **KHÔNG THÌ** không làm tính năng partner/HV đòi thêm.
3. ⏹ **NẾU** containment <43,4% **TRÊN** 200 job thử gần nhất **VÀ** từ ≥30 HV **THÌ** dừng bật tính tiền, không mở lớp mới; sửa prompt/nguồn 3 bài lab có tỉ lệ chuyển trợ giảng cao nhất rồi chạy lại eval. **KHÔNG THÌ** không nới định nghĩa "giải quyết xong", không tăng giá/bài.
4. **NẾU** inference ÷ doanh thu >38,5% **TRONG** 1 tháng **VÀ** partner ≥300 job tính tiền **THÌ** sprint tới khoá nút khi HV chạm trần 8 bài, cắt input fresh còn đoạn tô + 1 trang. **KHÔNG THÌ** không nâng trần hoá đơn/tăng giá đại trà.
5. **NẾU** eval thấp hơn baseline >5 điểm **TRÊN** 1 lần chạy 90 mẫu, hoặc ≥1 lỗi partner phải đính chính, **THÌ** trong 48h chuyển bài lỗi về chế độ "HV tự bật", gửi partner lỗi + bản sửa. **KHÔNG THÌ** không đổi sang model rẻ hơn hay cắt token tuần đó.

### Cổng gác 90 ngày (ngày 0 = 10/10/2026)

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 · 09/11 — **học** | Job thử của HV thật có log đủ lưu/bỏ/hỏi trợ giảng | ≥60 job (sai số containment ±12,7 điểm) | `pilot_jobs_log.csv` + email đồng ý pilot + `eval_round1.md` | Không có pilot trước 23/10 → **PIVOT** kênh (plugin Moodle tự cài); có pilot, <60 job → **FIX** 1 lần (bật mặc định) |
| 60 · 09/12 | Containment đo được trên ≥200 job thử | ≥54,2% (GM ≥60%) | Pilot Report 20/11 + log + bảng GM theo partner | 43,4–54,1% → **FIX** 1 lần · <43,4% → **PIVOT** thu hẹp loại bài lab |
| 90 · 08/01/2027 | Bài giải quyết xong **và đã tính tiền** / 30 ngày | ≥675 bài (150 HV × 75% × 6) | Hoá đơn gửi partner + log job | 450–674 → **FIX** reach 1 lần · <450 → **KILL** |

**KILL CRITERIA:** Dừng Tô Bài nếu đến **08/01/2027** có **<450 bài giải quyết xong và tính tiền trong 30 ngày** (MRR <$112,5 / 150 HV), hoặc containment **<43,4%** trên ≥300 job sau 1 lần FIX.

**CHƯA ĐO ĐƯỢC:** ① Containment thật — 75% là ước tính thô; cần log 3 trạng thái, có số ~02/11/2026. ② Chất lượng "giải thích đúng" — chưa có eval, chưa có SLA, partner chưa đồng ý định nghĩa; cần bộ eval 90 mẫu + 1 mentor kiểm, baseline sau đợt 2 (06/11/2026). ③ Sĩ số cohort (mẫu số reach) — phải xin partner, ghi vào email đồng ý pilot (trước 23/10). ④ Volume volatility — cần ≥3 tháng volume, ~01/2027. ⑤ Partner NRR — cần ≥12 tháng có doanh thu ([BM] trung vị SaaS 101%, Benchmarkit 2025). ⑥ Giờ dùng thật 21h–23h (Pain Moment) — mới là giả định phỏng vấn Day 17; có từ log timestamp tuần đầu pilot. ⑦ Chưa nói chuyện với partner — mọi số trên đều phụ thuộc việc này (hạn demo 23/10/2026).

<div style="page-break-after: always;"></div>

## Phụ lục [MH] — phép tính (nguồn: `LeThiChamAnh_Day22_model.xlsx`)

**Đầu vào chung:** P = $0,25/bài (`2_Pricing!B19`) · v = chi phí biến đổi/job thử = $0,041644 (`2_Pricing!B29` = LLM 0,0293 + infra 0,01 + retry 0,002344) · q = QA nội bộ/job thử = $0,0125 (`2_Pricing!B30`) · e = 0 (Biến thể A) · R = containment · GM mục tiêu 60% (`2_Pricing!B32`) · payback tối đa 12 tháng SMB (`4_Channel_Fit!B8`) · 6 bài xong/HV dùng/tháng, trần 8 bài (one-pager Day 22).

**[MH] 1 — Containment.** GM(R) = 1 − (v+q)/(P·R) = 1 − 0,216576/R.
GM = 60% → R = 0,216576/0,40 = **54,14%** (khớp `2_Pricing!B33`) · GM = 50% → R = 0,216576/0,50 = **43,32%** · Kiểm tra R = 75% → GM = 71,1% (khớp `2_Pricing!B21`).
→ 🟢 ≥54,2% · 🟡 43,4–54,1% · 🔴 <43,4%

**[MH] 2 — Inference ÷ doanh thu (đèn chi phí AI).** s = v/(P·R); COGS share = s·(1 + q/v) = 1,30·s (q/v = 0,300).
GM ≥60% ⇔ 1,30·s ≤ 0,40 ⇔ s ≤ **30,77%** · GM ≥50% ⇔ s ≤ **38,46%** · Mô hình (R = 75%): s = 0,041644/0,1875 = 22,2%.
Bắt thêm 2 thứ containment không thấy: token/job thật vượt giả định 3 lượt × 8.700 token, và job vượt trần 8 bài (tốn token, không tính tiền).
→ 🟢 ≤30,7% · 🟡 30,8–38,4% · 🔴 >38,5%

**[MH] 3 — End-user reach & MRR/HV.** Phát hiện: ARPU $225 (`4_Channel_Fit!B5`) = 150 HV × 6 × $0,25 → Day 22 ngầm giả định **100% HV đều dùng**.
MRR(r) = 225·r · CAC tối đa = MRR × 71,1% × 12 = 1.920·r.
MRR ≥ $225 ngay cả khi mọi HV dùng chạm trần 8 bài: 150·r·8·0,25 ≥ 225 → **r ≥ 75%** (MRR $168,75 ở mức 6 bài; CAC tối đa $1.440; MRR/HV $1,125).
r = 50% → MRR $112,5; CAC tối đa $960; nếu vẫn tiêu đủ $1.920 → payback = 1.920/(112,5 × 0,711) = **24 tháng** = 2× giới hạn SMB (MRR/HV $0,75).
→ reach 🟢 ≥75% · 🟡 50–75% · 🔴 <50% · MRR/HV 🟢 ≥$1,125 · 🟡 $0,75–1,124 · 🔴 <$0,75

**[MH] 4 — Time-to-first-end-user.** Pilot 40 HV (`5_90Day_Plan!B13`, giữa 30–50) bắt đầu ~26/10; cổng 30 = 09/11.
Job thử/ngày = 40 × 75% × 6 ÷ 75% ÷ 30 = **8**. Cổng 30 cần ≥60 job thử (95% CI containment = 1,96·√(0,25/60) = ±12,7 điểm → 75% vẫn tách được khỏi 54%) → cần 60/8 = **7,5 ngày** dùng thật trước 09/11 → job thật đầu tiên trễ nhất ~01/11 (≈7 ngày sau khi pilot bắt đầu). >14 ngày: cổng 30 chắc chắn trượt, Pilot Report 20/11 có <2 tuần dữ liệu.
→ 🟢 ≤7 · 🟡 8–14 · 🔴 >14 ngày

**[MH] 5 — Rev-share tối đa được nhường.** GM trước rev-share 71,1% − GM mục tiêu 60% = **11,1%** doanh thu (R = 75%). Nếu R thật = 60%: GM = 1 − 0,216576/0,60 = 63,9% → chỉ còn **3,9%**. → Không ký rev-share >11% với bên phân phối plugin Moodle khi chưa có containment đo được.

**Cổng 90 & kill:** 675 = 150 HV × 75% × 6 (reach 🟢); 450 = 150 × 50% × 6 (reach 🔴 → MRR $112,5).
