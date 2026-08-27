# Track 1 · Day 25 — AI Pricing · GTM · Evidence

> **Từ sản phẩm chạy được đến sản phẩm bán được.** Bài này trả lời ba câu mà demo không trả lời hộ được:
> khách lấy tiền từ ngân sách nào, tính tiền theo đơn vị gì, bán qua kênh nào — cộng một câu thứ tư:
> lấy gì để Procurement dám ký.

---

## Thông tin bài nộp

| | |
|---|---|
| **Họ và tên** | Lê Quang Huy |
| **MHV** | 2A202601821 |
| **Sản phẩm** | **WalletCare / FIN-05** — AI Agent CSKH ví điện tử & xử lý khiếu nại giao dịch (repo `P-121`, nhóm T121) |
| **Ngày lập mô hình** | 27/08/2026 · tỷ giá giả định 26.000 ₫/USD |
| **Value Metric** | **Hybrid** — phí nền + hai đơn giá theo ca **hoàn thành** |
| **Kênh 90 ngày đầu** | **Sales-Led** (named account) — đúng một kênh |
| **File Excel** | [`2A202601821_LeQuangHuy_Day25_model.xlsx`](2A202601821_LeQuangHuy_Day25_model.xlsx) |
| **One-Pager** | [`2A202601821_LeQuangHuy_Day25_onepager.docx`](2A202601821_LeQuangHuy_Day25_onepager.docx) · bản PDF cùng nội dung: [`…onepager.pdf`](2A202601821_LeQuangHuy_Day25_onepager.pdf) |
| **Log phản biện** | [`docs/critique-log.md`](docs/critique-log.md) — chạy §4.7.1 và §4.7.5, ghi accept/reject |

**Cả hai file đều dựng trên template chính chủ của Lab** (`Day25-AI-Product-GTM-Monetization-Model.xlsx`
và `Day25-AI-Product-GTM-One-Pager-Template.docx`), giữ nguyên toàn bộ công thức và bố cục gốc. Phần
phân tích vượt ra ngoài khuôn template được để trong các **khối mở rộng** đánh dấu rõ ở cuối mỗi tab,
không sửa một ô công thức nào của template.

---

## Kết luận một dòng

**Ở mức chất lượng đo được hôm nay, sản phẩm này chưa được phép bán theo bảng giá đề xuất — và mô hình
tài chính nói ra điều đó bằng một con số cụ thể, không bằng cảm giác.**

Bảng giá cần tỷ lệ hồ sơ điều tra được sếp ví duyệt *ngay lần trình đầu* đạt **≥ 43,26%**. Lượt eval có
provenance ngày **27/08/2026** đo được **1,03%** (1/97 ca kỳ vọng). Quy ra tỷ lệ hoàn thành job chỉ còn
**49,87%**, và ở mức đó bội số tụt xuống **2,79×** — trượt ngưỡng 3×. Vì vậy tháng đầu tiên của kế hoạch
90 ngày **cố ý đặt mục tiêu ký 0 hợp đồng**.

File chấm ghi thẳng nguyên nhân là **hệ thống** — `business_config` rỗng nên prompt rơi về khung chung và
agent gần như không mở hồ sơ ở bất kỳ ca nào — chứ không phải model yếu. Đó là khoảng cách đóng được,
nhưng phải đóng **trước** khi ký, không phải sau.

---

## Năm con số bắt buộc

| | Giá trị | Ô | |
|---|---:|---|:--:|
| **Cost/Job** | **0,0607 $ = 1.577 ₫** | `1_Cost_Job!B66` | |
| **Giá sàn** (3 × Cost/Job) | 0,1820 $ = 4.732 ₫ | `2_Pricing!B7` | |
| **Giá bán đề xuất** | **0,2309 $ = 6.004 ₫** | `2_Pricing!B19` | ✅ trong vùng neo |
| **Gross Margin** | **73,73%** · bội số **3,81×** | `2_Pricing!B21`, `B20` | ✅ |
| **Breakeven containment** | 44,70% | `2_Pricing!B33` | |
| Containment hiện tại | 68,06% *(mục tiêu)* — **đo thật 49,87%** | `1_Cost_Job!B10` | ❌ |

Mẫu số là **95.284 job hoàn thành**, không phải 140.000 ca đã thử.

---

## Bảng giá đề xuất

| Khoản | Giá | Đổi lấy cái gì |
|---|---:|---|
| Phí nền | **130.000.000 ₫/tháng** | Nạp KB riêng · connector MCP vào hệ thống ví · dashboard tenant · SLA 99,5% · log kiểm toán bất biến · báo cáo eval hằng quý · **không giới hạn seat** |
| Ca contained | **1.900 ₫** | Agent tự giải quyết xong, khách không mở lại trong 72h (email) / 2h (chat) |
| Hồ sơ duyệt lần đầu | **12.000 ₫** | Sếp ví ra quyết định cuối **ngay lần trình đầu**, không bấm “yêu cầu điều tra thêm” |

Hồ sơ bị trả về · ca lỗi kỹ thuật · ca chuyển ra người ngay từ đầu: **không tính là job, không tính tiền.**

Doanh thu **572,1tr ₫/ví/tháng** — bằng **17,6%** giá trị tạo ra cho ví, ROI của khách **5,7×**.

**Phát hiện đáng nói nhất của bảng giá:** tách riêng dòng usage ra khỏi phí nền thì bội số chỉ còn
**2,94× — trượt ngưỡng 3×**. Phí nền không phải khoản phụ thu cho tiện; nó là thứ kéo mô hình qua ngưỡng,
tức là một phần của cấu trúc.

---

## Decision Note — vì sao Hybrid, vì sao không Outcome

**Attribution 5/10 · Autonomy 3/10** → ma trận của template trỏ “SEAT hoặc HYBRID”. Ta chọn Hybrid.

Không chọn **Seat** vì âm biên: một CSKH có thể đẩy qua 4 hồ sơ/ngày hoặc 40 — chi phí biến thiên 10 lần
trong khi giá đứng yên. Đúng lý do GitHub Copilot phải bỏ mô hình cũ từ 01/06/2026.

Không chọn **Outcome**, và lý do là một con số chứ không phải một lập luận. Mô phỏng Biến thể B — ta nhận
trách nhiệm giao kết quả cuối thay vì để ví tự xử lý ca escalate — cho Gross Margin **−60,4%**, và cần tỷ
lệ hoàn thành **93,2%** mới về được 60%. Với sản phẩm mà HITL là bắt buộc theo Nghị định 52/2024 và Thông
tư 40/2024, 93% là bất khả thi. Intercom bán được 0,99 $/resolution vì Fin nói thẳng với người dùng cuối
và tự đóng ca; WalletCare không có quyền đó, và theo luật thì sẽ không bao giờ có.

**Một ranh giới cần nói rõ.** Đơn giá hồ sơ *trông* giống Outcome pricing nhưng không phải. Ta tính tiền
trên một state transition quan sát được trong hệ thống của chính khách — Attribution cho việc đó là 100%.
Outcome pricing là tính tiền trên một KPI kinh doanh mà ta nhận công (“ví tiết kiệm được X đồng”) —
Attribution cho việc đó ta chưa có, vì chưa có holdout trên lưu lượng thật. Đây đúng là cách Zendesk tách
*contained resolution* (không trừ hạn mức) khỏi *verified resolution* (có trừ, phải qua LLM kiểm chứng).

---

## Mô hình gãy ở đâu

**Gãy ở lao động người, không ở token.** LLM chỉ chiếm **23,1%** chi phí; QA nội bộ chiếm **35,2%** và là
khoản lớn nhất — lại là con số ít bằng chứng nhất, mới suy ra từ giai đoạn demo, chưa từng đo ở tải
140.000 ca/tháng.

Ngưỡng cụ thể: **Gross Margin tụt dưới 50% khi tỷ lệ hoàn thành job rơi xuống dưới 35,8%, hoặc khi chi
phí lao động QA sai hơn 2,9 lần.**

Hệ quả thứ hai: **chọn model không phải chi tiết kỹ thuật, nó là biến sống còn.** Cùng khối lượng token
này, một model tuyến đầu đắt gấp khoảng 3,5 lần `deepseek-v4-flash` và kéo bội số xuống dưới 2,1×. Ngược
lại, kịch bản 100% lưu lượng rơi vào khung giá peak của DeepSeek chỉ hạ bội số xuống 3,55× — rủi ro nhỏ
hơn nhiều so với rủi ro đổi nhà cung cấp.

**Vì sao GM 73,7% cao hơn benchmark AI-native 52–53%** — ba lý do kiểm chứng được, không phải vì ta giỏi
hơn thị trường: (1) `deepseek-v4-flash` rẻ hơn model tuyến đầu khoảng 3,5 lần; (2) lao động QA tại Việt
Nam 3,30 $/giờ so với 25–40 $/giờ ở Mỹ; (3) Biến thể A — chi phí người xử lý ca escalate nằm ở phía ví,
đúng như ràng buộc HITL bắt buộc quy định. Đổi bất kỳ điều nào trong ba điều đó, GM sập ngay.

---

## Kênh: Sales-Led, và số học nói vì sao

| | |
|---|---:|
| ARPU / tháng | **22.002 $ = 572,1tr ₫** |
| Ngân sách CAC (ARPU × GM × 24 tháng) | **389.325 $** |
| CAC thực tế (cost-per-opportunity 11.200 $ ÷ win rate 25%) | 44.800 $ = 1,16 tỷ ₫ |
| Lệch | **CAC chỉ bằng 11,5% ngân sách** |
| CAC payback · LTV/CAC | 2,76 tháng · 18,1× |
| Deal / AE / ngày làm việc | 0,0012 |

Một hợp đồng trả xong hơn ba năm quota của một AE. Nên **ràng buộc thật không phải năng suất bán hàng mà
là TAM khoảng 40 ví đang hoạt động tại Việt Nam** cộng chu kỳ mua fintech 6–12 tháng. Đây là bài toán phủ
tài khoản, không phải bài toán thông lượng.

**PLG bị loại vì lý do cấu trúc**, không phải vì kém hiệu quả: không ví nào cho một tài khoản tự đăng ký
đọc sổ cái giao dịch của khách hàng họ.

**Partner-Led không nằm trong 90 ngày, và lý do phải nói thẳng:** một đội sáu người chưa có khách trả tiền
**không có đường đặt lịch** với NAPAS hay một nhà tích hợp lớn như FPT IS. Viết “xin lịch gặp NAPAS trong
2 tuần” vào kế hoạch là tự lừa mình — một bước chỉ được tính là bước nếu đội có đường thực hiện nó ngay
tuần này. Phép phủ định **khả thi**: hỏi đầu mối ZaloPay đã có đúng một câu — *“khi ví chọn nhà cung cấp
cho khâu tra soát, các anh có bao giờ mua qua giới thiệu của NAPAS hoặc của SI không, hay luôn mua
thẳng?”*. Tốn một tin nhắn, không tốn một chiến dịch.

**Quan hệ đã có, nói đúng mức:** ZaloPay — PO của nhóm đã gặp 2 lần để lấy góc nhìn nghiệp vụ và phản hồi
demo. Đây chưa phải một cuộc nói chuyện thương mại, chưa có người mua được xác định, chưa có ngân sách.

---

## Kế hoạch 90 ngày

| Giai đoạn | Mục tiêu | KPI |
|---|---|---|
| **T1 · 09/2026**<br>Học, không bán | Đóng lỗ hổng **đo lường** trước lỗ hổng sản phẩm: viết runner T3/T4/T5, seed `business_config`, sửa định tuyến skill để agent mở được hồ sơ | `missed_expected_ticket` 96/97 → ≤ 10/97 · blocking clean_rate 94,83% → 100% · PDPA leak 4 ca → 0 · `tools_required_satisfied` 21,55% → ≥ 70% · **hợp đồng ký: 0 (cố ý)** |
| **T2–T3 · 10–11/2026**<br>Đòn bẩy trên 1 ví | 4 tuần shadow rồi 4 tuần live lớp A ở đúng một ví | Hồ sơ duyệt-lần-đầu ≥ 43,26% · Cost/Job ≤ 0,065 $ · lao động người ≤ 55% chi phí · 2 cuộc gặp cấp trưởng bộ phận CSKH |
| **T4+ · từ 12/2026**<br>Mở rộng có điều kiện | Chỉ mở rộng khi một ví đạt tỷ lệ hoàn thành ≥ 68% **ba tháng liên tiếp** VÀ có Pilot Report được khách xác nhận | Điều kiện đạt / chưa đạt — nhị phân, không thương lượng |

---

## Evidence Pack — thành thật về khoảng trống

| Tài sản | Trạng thái | Hạn chót |
|---|---|---|
| **Eval Results** | **Một phần.** Golden 118 ca + held-out 49 ca, harness chạy lại được, thẻ điểm 3 mức, và từ 26/08/2026 mỗi file chấm mang **provenance** (commit `10d30e5` + sha256 của bộ chấm, file run, bộ đáp án, dataset). `hitl_ticket_without_confirm = 0` và lần này quan sát được thật. **Thiếu:** `report.md` vẫn trống, chưa chấm held-out, blocking 94,83% chưa đạt ngưỡng 0 vi phạm, chưa đo resolution. | 30/09/2026 |
| **Risk Checklist** | **Có nguyên liệu, chưa có bản cho sản phẩm này.** Bản Day 22 làm trên TriageMate (y tế) nên không dùng lại được. Sẵn có: 6 ràng buộc bắt buộc ở Brief §7, 6 rào cứng trong mã nguồn, NĐ 52/2024, TT 40/2024, NĐ 13/2023. **Thiếu:** văn bản trả lời ba câu Procurement, DPA mẫu; **chưa có SOC 2 và sẽ chưa có trong 12 tháng tới**. | 15/09/2026 |
| **Pilot Report** | **Chưa có.** Chưa ví nào chạy pilot. | Ký pilot 15/10/2026 · báo cáo 30/11/2026 |

**Bài test người lạ: chưa có số thật** — bài làm cá nhân, chưa đưa cho nhóm khác đọc, và không điền số
bịa vào ô đó. Phần tự kiểm được ghi trong `5_90Day_Plan` (dòng 29–32): cả ba câu đều trả lời được, nhưng
có 2 chỗ phải đọc lại lần hai — dễ nhầm giá sàn với giá bán, và vì sao GM 73,7% mà vẫn kết luận chưa được
ký. Đã sửa bằng cách đưa phán quyết lên ngay đầu One-Pager.

---

## Bài học đắt nhất, và nó thuộc về đúng bài Day 25 này

Thư mục `eval/results/` của P-121 chứa một cảnh báo mà bài Pricing nên đọc: cùng một sản phẩm, cùng một
ngày, hai bộ chấm khác nhau cho ra **25%** và **94,8%** — và không cách nào biết vì sao, vì file cũ không
ghi phiên bản bộ chấm. Một lượt chạy hỏng vì môi trường (bảng phiên rỗng, mọi tool trả lỗi) lại được chấm
**cao** ở tầng vi phạm chặn, vì không tra được thì không có số nào để bịa. Một lượt bị lỗi 429 ở 70/118 ca
được chấm **99,14%**, cao hơn cả lượt chạy thật.

Kết luận rất gọn: nếu Value Metric của bạn tính tiền theo kết quả, thì con số kết quả phải **tái lập
được**, không chỉ phải **tồn tại**. Bán Outcome trên một con số không có provenance là ký hợp đồng dựa
trên một con số ngẫu nhiên.

---

## Đính chính mang sang từ Day 24

| Khoản | Day 24 | Day 25 | Vì sao |
|---|---|---|---|
| CAC | 300tr ₫ | **1,16 tỷ ₫** | Benchmark ICONIQ 2026 (cost-per-opportunity 11.200 $, win rate 25%) cho thấy con số Day 24 thấp hơn thực tế ~3,9 lần. Kể cả sau đính chính, LTV/CAC vẫn 18,1× và payback 2,76 tháng. |
| ARPU | 450tr ₫ | **572,1tr ₫** | Day 24 định giá theo hợp đồng phẳng. Day 25 định giá theo **đơn vị hoàn thành**, nên doanh thu đi theo khối lượng công việc thật sự giao được. |
| Containment | “không ăn vào COGS” | vẫn đúng, nhưng **ăn vào mẫu số** | Bot đốt token cho cả 140.000 ca dù ca đó có hoàn thành hay không. Day 24 đúng ở phía chi phí; Day 25 bổ sung phía còn lại: tỷ lệ hoàn thành quyết định Cost/Job vì nó là mẫu số. |

---

## Giới hạn đã biết của mô hình

1. **Mix 62/26/12 giữa ba lớp ca là ước tính từ phân bố 118 ca golden set**, chưa đo trên lưu lượng thật.
   Nằm trong KPI tháng 1.
2. **Containment lớp A 80% chưa từng được đo.** Bộ eval hiện chấm vi phạm chặn và tuân thủ hợp đồng, không
   chấm resolution. 80% là mục tiêu pilot, không phải kết quả.
3. **Đơn giá lao động QA 3,30 $/giờ và khối lượng review 10% suy ra từ giai đoạn demo.** Vì đây là 35%
   chi phí, sai số ở đây đắt hơn mọi sai số khác.
4. **Ô S3 của template dùng một hội thoại bình quân gia quyền**, trong khi chi phí thật phải tính riêng ba
   lớp ca. Hàm chi phí lồi theo (số lượt × token) nên bình quân làm hụt **9,16%** chi phí LLM
   (1.770,74 $ so với 1.949,20 $). Mô hình giữ con số của template để công thức gốc chạy đúng, và ghi lại
   khoảng lệch ở khối mở rộng ① của `1_Cost_Job` thay vì giấu. Tính đúng từng lớp thì Cost/Job lên
   0,0625 $ và bội số còn 3,69× — vẫn qua ngưỡng.
5. **Overhead phân bổ giả định 4 hợp đồng ví đang chạy.** Hôm nay con số thật là 0.
6. **Giá DeepSeek có cấu trúc peak/off-peak**, và khung peak của họ trùng gần khít giờ hành chính Việt
   Nam. Mô hình dùng tỷ lệ 65% peak — cũng là một ước tính.

---

## Kiểm chứng số học

Vì file Excel do script sinh ra không mang giá trị cache, tôi viết một bộ tính riêng đánh giá **toàn bộ
93 ô công thức** trong workbook và đối chiếu **33 chỉ số chính** với mô hình Python độc lập. Kết quả:
**0 lỗi, 33/33 khớp tuyệt đối.** Bộ tính này cũng bắt được một lỗi thật trong bản đầu — vài ô ghi chú mở
đầu bằng dấu `=` khiến Excel hiểu nhầm là công thức và hiện `#NAME?`. Đã sửa.

Excel, LibreOffice và Google Sheets đều tính lại công thức khi mở file. Tab `0_README` có thêm khối tóm
tắt các con số chính kèm địa chỉ ô gốc, phòng trường hợp mở bằng trình xem nhẹ không tính công thức.

---

## Cấu trúc repo

```
├── 2A202601821_LeQuangHuy_Day25_model.xlsx      # template chính chủ đã điền, 7 tab + khối mở rộng
├── 2A202601821_LeQuangHuy_Day25_onepager.docx   # template One-Pager chính chủ đã điền
├── 2A202601821_LeQuangHuy_Day25_onepager.pdf    # bản PDF xuất từ chính file .docx trên
├── docs/critique-log.md                         # chạy prompt §4.7, ghi accept/reject
├── ai-support-log.md                            # log dùng AI
└── README.md
```

**Quy ước màu trong Excel** (theo template): 🟡 vàng = ô đầu vào · ⬜ xám = công thức tự tính · 🟩 xanh =
đạt ngưỡng · 🟥 đỏ = không đạt, phải sửa giả định chứ không sửa giá cho đẹp.

---

## Nguồn số liệu

**Giá API — tự mở lại trang gốc, kiểm tra 27/08/2026:**
[DeepSeek](https://api-docs.deepseek.com/quick_start/pricing) ·
[Anthropic](https://platform.claude.com/docs/en/about-claude/pricing)

Hai đính chính so với tài liệu Lab, đều ghi trong tab `6_Benchmarks`:

- Tài liệu đánh dấu Claude Sonnet 5 ở mức 2/10 $ là giá khuyến mại sẽ tăng lên 3/15 $ từ 01/09/2026. Trang
  giá ngày 27/08/2026 cho biết mức 2/10 $ **đã thành giá chuẩn và đợt tăng đó sẽ không diễn ra**.
- Tài liệu ghi Zendesk 1,50 $/automated resolution. Trang tài liệu chính thức **không công bố đơn giá** —
  con số đó là từ blog. Trang này chỉ nêu ba bậc và cửa sổ kết thúc hội thoại.

**Benchmark giá sản phẩm — tự kiểm tra 27/08/2026:** [Intercom Fin](https://fin.ai/pricing/) ·
[Zendesk](https://support.zendesk.com/hc/en-us/articles/9570369117338-About-automated-resolution-tiers)

**Benchmark biên lợi nhuận & GTM (theo §3.5 tài liệu Lab, chốt 26/08/2026):** ICONIQ State of AI 2026 ·
ICONIQ State of GTM in 2026 · Bessemer State of the Cloud 2024 · David Skok SaaS Metrics 2.0 · Tomasz Tunguz

**Bằng chứng lấy từ chính sản phẩm:** `P-121 · eval/results/run-2026-08-27-sau-seed-scored.json`
(có provenance, commit `10d30e5`) · `src/core/config.py` · `FIN05-Brief.md`

**Kế thừa từ các Day trước:** Day 20–21 (hạ tầng eval) · Day 22 (khung Responsible AI) ·
Day 23 (core action và NSM — nguồn của định nghĩa “1 job”) · Day 24 (khối lượng, churn, cấu trúc chi phí)
