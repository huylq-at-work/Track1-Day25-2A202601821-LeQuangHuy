# Track 1 · Day 25 — AI Pricing · GTM · Evidence

> **Từ sản phẩm chạy được đến sản phẩm bán được.** Bài này trả lời ba câu mà demo không trả lời hộ được:
> khách lấy tiền từ ngân sách nào, tính tiền theo đơn vị gì, và bán qua kênh nào — cộng một câu thứ tư:
> lấy gì để Procurement dám ký.

---

## Thông tin bài nộp

| | |
|---|---|
| **Họ và tên** | Lê Quang Huy |
| **MHV** | 2A202601821 |
| **Sản phẩm** | **WalletCare / FIN-05** — AI Agent CSKH ví điện tử & xử lý khiếu nại giao dịch (repo `P-121`, nhóm T121, Build Phase Cohort 3) |
| **Ngày lập mô hình** | 27/08/2026 · tỷ giá giả định 26.000 ₫/USD |
| **Value Metric** | **Hybrid** — phí nền + hai đơn giá theo ca **hoàn thành** |
| **Kênh 90 ngày đầu** | **Sales-Led** (named account / ABM) — đúng một kênh |
| **File Excel** | [`2A202601821_LeQuangHuy_Day25_model.xlsx`](2A202601821_LeQuangHuy_Day25_model.xlsx) — 7 tab |
| **One-Pager** | [`2A202601821_LeQuangHuy_Day25_onepager.pdf`](2A202601821_LeQuangHuy_Day25_onepager.pdf) — 1 trang A4 (bản HTML nguồn ở [`onepager/`](onepager/)) |
| **Log phản biện** | [`docs/critique-log.md`](docs/critique-log.md) — chạy §4.7.1 và §4.7.5, ghi accept/reject |

---

## Kết luận một dòng

**Ở mức chất lượng đo được hôm nay, sản phẩm này chưa được phép bán theo bảng giá đề xuất — và mô hình
tài chính nói ra điều đó bằng một con số cụ thể, chứ không bằng cảm giác.**

Bảng giá chỉ đứng được khi tỷ lệ hồ sơ điều tra được sếp ví duyệt *ngay lần trình đầu* đạt **≥ 46,67%**.
Lượt eval có provenance ngày **27/08/2026** đo được **1,03%** (1/97 ca kỳ vọng). Vì vậy tháng đầu tiên của
kế hoạch 90 ngày **cố ý đặt mục tiêu ký 0 hợp đồng**.

File chấm chỉ ra nguyên nhân là **hệ thống** — `business_config` rỗng nên prompt rơi về khung chung, agent
gần như không mở hồ sơ — chứ không phải model yếu. Đó là khoảng cách đóng được, không phải bức tường.
Nhưng nó phải được đóng **trước** khi ký, không phải sau.

---

## Năm con số bắt buộc

| | Giá trị | Ngưỡng | |
|---|---:|---|:--:|
| **Cost/Job** | **0,0627 $ = 1.629 ₫** | chia cho 95.284 job **hoàn thành**, không phải 140.000 ca thử | |
| **Giá sàn** (3 × Cost/Job) | 0,1880 $ = 4.888 ₫ | — | |
| **Giá bán bình quân / job** | **0,2309 $ = 6.004 ₫** | nằm giữa sàn 4.888 ₫ và trần 8.523 ₫ | ✅ |
| **Gross Margin** | **72,86%** | ≥ 60% | ✅ |
| **Breakeven** — tỷ lệ hồ sơ duyệt-lần-đầu | **≥ 46,67%** | đo thật 27/08/2026: **1,03%** | ❌ |

Chia nhầm cho số ca **đã thử** thay vì ca **hoàn thành** làm Cost/Job trông rẻ hơn thực tế **31,9%**.

---

## Bảng giá đề xuất

| Khoản | Giá | Đổi lấy cái gì |
|---|---:|---|
| Phí nền | **130.000.000 ₫/tháng** | Nạp KB riêng · connector MCP vào hệ thống ví · dashboard tenant · SLA 99,5% · log kiểm toán bất biến · báo cáo eval hằng quý · **không giới hạn seat** |
| Ca contained | **1.900 ₫** | Agent tự giải quyết xong với khách, khách không mở lại trong 72h (email) / 2h (chat) |
| Hồ sơ duyệt lần đầu | **12.000 ₫** | Sếp ví ra quyết định cuối **ngay lần trình đầu**, không bấm “yêu cầu điều tra thêm” |

Hồ sơ bị trả về · ca lỗi kỹ thuật · ca chuyển ra người ngay từ đầu: **không tính là job, không tính tiền.**

Doanh thu **572,1tr ₫/ví/tháng** — bằng **17,6%** giá trị tạo ra cho ví, ROI của khách **5,7×**.

---

## Decision Note — vì sao Hybrid, vì sao không Outcome

**Attribution 2/5, Autonomy 1/5.** Ma trận trỏ SEAT/HYBRID; ta chọn Hybrid.

Không chọn **Seat** vì âm biên: một CSKH có thể đẩy qua 4 hồ sơ/ngày hoặc 40 — chi phí biến thiên 10 lần
trong khi giá đứng yên. Đây đúng là lý do GitHub Copilot phải bỏ mô hình cũ từ 01/06/2026.

Không chọn **Outcome**, và lý do là một con số chứ không phải một lập luận. Mô phỏng Biến thể B — ta nhận
trách nhiệm giao kết quả cuối thay vì để ví tự xử lý ca escalate — cho ra Gross Margin **−61,3%**, và cần
tỷ lệ hoàn thành **94,1%** mới về được 60%. Với sản phẩm mà HITL là bắt buộc theo Nghị định 52/2024 và
Thông tư 40/2024, 94% là bất khả thi. Intercom bán được 0,99 $/resolution vì Fin nói thẳng với người dùng
cuối và tự đóng ca; WalletCare không có quyền đó, và sẽ không bao giờ có.

**Một ranh giới cần nói rõ.** Đơn giá hồ sơ *trông* giống Outcome pricing nhưng không phải. Ta tính tiền
trên một state transition quan sát được trong hệ thống của chính khách — Attribution cho việc đó là 100%.
Outcome pricing là tính tiền trên một KPI kinh doanh mà ta nhận công (“ví tiết kiệm được X đồng”) —
Attribution cho việc đó ta chưa có, vì chưa có holdout trên lưu lượng thật.

---

## Mô hình gãy ở đâu

| Cú sốc | Bội số | GM | |
|---|---:|---:|:--:|
| Cơ sở | 3,68× | 72,86% | ✅ |
| **Lao động người sai gấp 2** | 2,54× | 60,61% | ❌ |
| Hồ sơ duyệt-lần-đầu 71% → 35,5% | 2,69× | 62,77% | ❌ |
| Đổi sang Claude Haiku 4.5 | 1,97× | 49,19% | ❌ |
| Bỏ prompt caching | 2,48× | 59,67% | ❌ |

**Con số giết mô hình là lao động người, không phải token.** QA nội bộ cộng CSM chiếm **54% COGS**, tương
đương gần 5 FTE cho *một* hợp đồng — và đó là con số chưa từng được đo ở tải 140.000 ca/tháng, mới chỉ suy
ra từ giai đoạn demo.

Hệ quả thứ hai đáng nói: **chọn model không phải chi tiết kỹ thuật, nó là biến sống còn.** Chuyển từ
deepseek-v4-flash sang một model tuyến đầu làm bội số rơi từ 3,68× xuống 1,97×. Ngược lại, kịch bản 100%
lưu lượng rơi vào khung giá peak của DeepSeek chỉ hạ GM xuống 70,85% — rủi ro nhỏ hơn nhiều so với rủi ro
đổi nhà cung cấp.

**Vì sao GM 72,9% cao hơn benchmark AI-native 52–53%** — ba lý do kiểm chứng được, không phải vì ta giỏi
hơn thị trường: (1) deepseek-v4-flash rẻ hơn model tuyến đầu khoảng 3,5 lần cho đúng khối lượng token này;
(2) lao động QA tại Việt Nam 3,30 $/giờ so với 25–40 $/giờ ở Mỹ; (3) Biến thể A — chi phí người xử lý ca
escalate nằm ở phía ví, đúng như ràng buộc HITL bắt buộc quy định. Đổi bất kỳ điều nào trong ba điều đó,
GM sập ngay.

---

## Kênh: Sales-Led, và số học nói vì sao

| | |
|---|---:|
| Ngân sách CAC (ARPU × GM × 24 tháng) | **384.742 $** |
| CAC thực tế (cost-per-opportunity 11.200 $ ÷ win rate 25%) | 44.800 $ |
| Chênh lệch | **dư 8,59×** |
| CAC payback · LTV/CAC | 2,79 tháng · 17,9× |
| Deal / AE / ngày làm việc | 0,0012 |

Một hợp đồng trả xong hơn ba năm quota của một AE. Nên **ràng buộc thật không phải năng suất bán hàng mà
là TAM khoảng 40 ví đang hoạt động tại Việt Nam** cộng chu kỳ mua fintech 6–12 tháng. Đây là bài toán phủ
tài khoản, không phải bài toán thông lượng.

**PLG bị loại vì lý do cấu trúc**, không phải vì kém hiệu quả: không ví nào cho một tài khoản tự đăng ký
đọc sổ cái giao dịch của khách hàng họ.

**Partner-Led hoãn sang tháng 4, và có tên cụ thể:** NAPAS (mọi khiếu nại chạm ngân hàng đều đi qua quy
trình tra soát của họ) và FPT IS / Viettel Solutions. **Trạng thái: chưa liên hệ cả hai.** Chưa liên hệ thì
chưa phải là một kênh. Phép phủ định trong 2 tuần: xin 30 phút với ban hợp tác NAPAS và hỏi đúng một câu về
điều kiện giới thiệu — không đặt được lịch thì gạch khỏi kế hoạch, không giữ lại cho đẹp slide.

**Quan hệ đã có, nói đúng mức:** ZaloPay — PO của nhóm đã gặp 2 lần để lấy góc nhìn nghiệp vụ và phản hồi
demo. Đây chưa phải một cuộc nói chuyện thương mại, chưa có người mua được xác định, chưa có ngân sách.

---

## Kế hoạch 90 ngày

| Giai đoạn | Mục tiêu | KPI |
|---|---|---|
| **T1 · 09/2026**<br>Học, không bán | Đóng lỗ hổng **đo lường** trước lỗ hổng sản phẩm: viết runner T3/T4/T5, xử lý nguyên nhân hệ thống khiến agent không mở hồ sơ | `missed_expected_ticket` 96/97 → ≤ 10/97 · blocking clean_rate 94,83% → 100% · PDPA leak 4 ca → 0 · `tools_required_satisfied` 21,55% → ≥ 70% · **hợp đồng ký: 0 (cố ý)** |
| **T2–T3 · 10–11/2026**<br>Đòn bẩy trên 1 ví | 4 tuần shadow rồi 4 tuần live lớp A ở đúng một ví | Hồ sơ duyệt-lần-đầu ≥ 46,67% · Cost/Job ≤ 0,065 $ · lao động người ≤ 55% COGS · 2 cuộc gặp cấp trưởng bộ phận CSKH |
| **T4+ · từ 12/2026**<br>Mở rộng có điều kiện | Chỉ mở rộng khi một ví đạt tỷ lệ hoàn thành ≥ 68% **ba tháng liên tiếp** VÀ có Pilot Report được khách xác nhận | Điều kiện đạt / chưa đạt — nhị phân, không thương lượng |

---

## Evidence Pack — thành thật về khoảng trống

| Tài sản | Trạng thái | Hạn chót |
|---|---|---|
| **Eval Results** | **CÓ MỘT PHẦN.** Golden 118 ca + held-out 49 ca, harness chạy lại được, thẻ điểm 3 mức, và từ 26/08/2026 mỗi file chấm mang khối **provenance** (commit + sha256 của bộ chấm, file run, bộ đáp án, dataset). `hitl_ticket_without_confirm = 0` và lần này quan sát được thật. **Thiếu:** `report.md` vẫn trống, chưa chấm held-out, blocking 94,83% chưa đạt ngưỡng 0 vi phạm, chưa đo resolution. | 30/09/2026 |
| **Risk Checklist** | **CÓ NGUYÊN LIỆU, CHƯA CÓ BẢN CHO SẢN PHẨM NÀY.** Bản Day 22 làm trên TriageMate (y tế) nên không dùng lại được. Sẵn có: 6 ràng buộc bắt buộc ở Brief §7, 6 rào cứng trong mã nguồn, NĐ 52/2024, TT 40/2024, NĐ 13/2023. **Thiếu:** văn bản trả lời ba câu Procurement, DPA mẫu; **chưa có SOC 2 và sẽ chưa có trong 12 tháng tới** — nói thẳng chứ không né. | 15/09/2026 |
| **Pilot Report** | **CHƯA CÓ.** Chưa ví nào chạy pilot. | Ký pilot 15/10/2026 · báo cáo 30/11/2026 |

---

## Bài học đắt nhất, và nó thuộc về đúng bài Day 25 này

Thư mục `eval/results/` của P-121 chứa một cảnh báo mà bài Pricing nên đọc: cùng một sản phẩm, cùng một
ngày, hai bộ chấm khác nhau cho ra **25%** và **94,8%** — và không cách nào biết vì sao, vì file cũ không
ghi phiên bản bộ chấm. Một lượt chạy hỏng vì môi trường (bảng phiên rỗng, mọi tool trả lỗi) lại được chấm
**cao** ở tầng vi phạm chặn, vì không tra được thì không có số nào để bịa. Một lượt bị lỗi 429 ở 70/118 ca
được chấm **99,14%**, cao hơn cả lượt chạy thật.

Với bài này, kết luận rất gọn: nếu Value Metric của bạn tính tiền theo kết quả, thì con số kết quả phải
**tái lập được**, không chỉ phải **tồn tại**. Bán Outcome trên một con số không có provenance là ký hợp
đồng dựa trên một con số ngẫu nhiên.

---

## Đính chính mang sang từ Day 24

| Khoản | Day 24 | Day 25 | Vì sao |
|---|---|---|---|
| CAC | 300tr ₫ | **1,16 tỷ ₫** | Benchmark ICONIQ 2026 (cost-per-opportunity 11.200 $, win rate 25%) cho thấy con số Day 24 thấp hơn thực tế ~3,9 lần. Kể cả sau đính chính, LTV/CAC vẫn 17,9× và payback 2,79 tháng. |
| ARPU | 450tr ₫ | **572,1tr ₫** | Day 24 định giá theo hợp đồng phẳng. Day 25 định giá theo **đơn vị hoàn thành**, nên doanh thu đi theo khối lượng công việc thật sự giao được. |
| Containment | "không ăn vào COGS" | vẫn đúng, nhưng **ăn vào mẫu số** | Bot đốt token cho cả 140.000 ca dù ca đó có hoàn thành hay không. Day 24 kết luận đúng ở phía chi phí; Day 25 bổ sung phía còn lại: tỷ lệ hoàn thành quyết định Cost/Job vì nó là mẫu số. |

---

## Giới hạn đã biết của mô hình

1. **Mix 62/26/12 giữa ba lớp ca là ước tính từ phân bố 118 ca golden set, chưa đo trên lưu lượng thật.**
   Đây là đầu vào nhạy thứ ba của mô hình và nằm trong KPI tháng 1.
2. **Containment lớp A 80% chưa từng được đo.** Bộ eval hiện chấm vi phạm chặn và tuân thủ hợp đồng, không
   chấm resolution. Con số 80% là mục tiêu pilot, không phải kết quả.
3. **Đơn giá lao động QA 3,30 $/giờ và khối lượng review 10% suy ra từ giai đoạn demo**, chưa chạy ở tải
   140.000 ca/tháng. Vì đây là 45% COGS, sai số ở đây đắt hơn mọi sai số khác.
4. **Overhead phân bổ giả định 4 hợp đồng ví đang chạy.** Hôm nay con số thật là 0. Cột "biên sau overhead
   64,34%" chỉ có nghĩa ở trạng thái đã có 4 hợp đồng.
5. **Giá DeepSeek có cấu trúc peak/off-peak**, và khung peak của họ trùng gần khít giờ hành chính Việt Nam.
   Mô hình dùng tỷ lệ 65% peak — cũng là một ước tính.

---

## Cấu trúc repo

```
├── 2A202601821_LeQuangHuy_Day25_model.xlsx      # 7 tab: README · Cost_Job · Pricing · Value_Metric · Channel_Fit · 90Day_Plan · Benchmarks
├── 2A202601821_LeQuangHuy_Day25_onepager.pdf    # One-Pager 1 trang A4
├── onepager/onepager.html                       # nguồn HTML của One-Pager
├── docs/critique-log.md                         # chạy prompt §4.7, ghi accept/reject
├── ai-support-log.md                            # log dùng AI
└── README.md
```

**Quy ước màu trong Excel:** 🟡 vàng = ô đầu vào bạn điền · ⬜ xám = công thức tự tính · 🟩 xanh = đạt ngưỡng
· 🟥 đỏ = không đạt, phải sửa giả định chứ không sửa giá cho đẹp.

---

## Nguồn số liệu

**Giá API — tự mở lại trang gốc, kiểm tra 27/08/2026:**
[DeepSeek](https://api-docs.deepseek.com/quick_start/pricing) ·
[Anthropic](https://platform.claude.com/docs/en/about-claude/pricing)

Một đính chính so với tài liệu Lab: tài liệu đánh dấu Claude Sonnet 5 ở mức 2/10 $ là giá khuyến mại sẽ tăng
lên 3/15 $ từ 01/09/2026. Trang giá ngày 27/08/2026 cho biết mức 2/10 $ **đã trở thành giá chuẩn và đợt tăng
đó sẽ không diễn ra**. Đây đúng là lý do §3.3 bắt tự mở lại trang giá thay vì chép số trong slide.

**Benchmark giá sản phẩm:** [Intercom Fin](https://fin.ai/pricing/) (kiểm tra 27/08/2026) ·
[Zendesk](https://www.zendesk.com/blog/ai/agentic-ai/outcome-based-pricing/) ·
[Salesforce Agentforce](https://www.salesforce.com/agentforce/pricing/) ·
[GitHub Copilot](https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/)

**Benchmark biên lợi nhuận & GTM:** ICONIQ State of AI 2026 · ICONIQ State of GTM in 2026 ·
Bessemer State of the Cloud 2024 · David Skok SaaS Metrics 2.0 · Tomasz Tunguz (2016)

**Bằng chứng lấy từ chính sản phẩm:** `P-121 · eval/results/run-2026-08-27-sau-seed-scored.json`
(có provenance, commit `10d30e5`) · `src/core/config.py` · `FIN05-Brief.md`

**Kế thừa từ các Day trước:** Day 20–21 (hạ tầng eval) · Day 22 (khung Responsible AI) ·
Day 23 (định nghĩa core action và NSM — nguồn của định nghĩa “1 job”) · Day 24 (khối lượng, churn, cấu trúc chi phí)
