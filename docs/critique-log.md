# Log phản biện — chạy prompt §4.7

> Yêu cầu của Final Checklist mục 10: chạy ít nhất 2 prompt ở §4.7 và ghi lại accept / reject / partial.
> Đã chạy **§4.7.1 — Cost/Job Stress Test** và **§4.7.5 — One-Pager Defensibility Check**.
>
> **Công cụ:** Claude Opus 5, phiên làm việc ngày 27/08/2026.
> **Nguyên tắc áp dụng:** AI là công cụ phản biện, không phải tác giả. Mọi sửa đổi bên dưới do tôi quyết định
> và viết lại bằng lời của mình; không câu nào được chép nguyên văn từ output của AI vào bài nộp.

---

## §4.7.1 — Cost/Job Stress Test

Chạy trên bản nháp đầu của Tab 1, ở thời điểm mô hình mới có ba khoản: token LLM, infra, và một dòng HITL ước lượng.

### 1 · Thiếu hạng mục chi phí

| # | Điểm phản biện | Quyết định | Đã làm gì |
|---|---|:--:|---|
| 1.1 | Thiếu chi phí **chạy lại bộ eval**: eval không tự do, và với sản phẩm bán theo kết quả thì nó là chi phí phục vụ khách chứ không phải R&D | **ACCEPT** | Thêm dòng S7b 23 $/tháng cho 4 lượt chạy dev + judge (judge tốn ~220k token cho 118 ca) |
| 1.2 | Thiếu **CSM / solutions**: hợp đồng B2B enterprise không tự vận hành | **ACCEPT** | Thêm 0,4 FTE = 461,54 $/tháng vào COGS, không vào overhead — support khách là COGS |
| 1.3 | Thiếu **compliance phân bổ** và **bảo trì prompt / skill / guard** | **ACCEPT** | Thêm 120,19 $ + 96,15 $/tháng, phân bổ trên 4 hợp đồng |
| 1.4 | Thiếu **log retention và observability**: ta cam kết giữ log 90 ngày trong Evidence Pack thì phải trả tiền cho nó | **ACCEPT** | Tách thành hai dòng riêng trong S5 thay vì gộp vào "infra" một cục |
| 1.5 | Đề xuất thêm chi phí **fine-tuning / retraining định kỳ** | **REJECT** | WalletCare không fine-tune. Toàn bộ hành vi nằm ở prompt lắp động, skill và guard — chi phí đó đã nằm ở dòng "bảo trì prompt/skill/guard". Thêm một dòng retraining nữa là đếm hai lần cho cùng một việc. |
| 1.6 | Đề xuất tính chi phí **egress** | **PARTIAL** | Có, nhưng nhỏ và đã nằm trong dòng object storage. Không tách riêng để tránh làm bảng dài mà không đổi kết luận. Ghi lại ở đây để người chấm biết là đã cân nhắc, không phải bỏ sót. |

### 2 · Kiểm tra mẫu số

**Điểm phản biện:** *"Bạn đang chia cho job ĐÃ THỬ hay job HOÀN THÀNH? Tính lại và nói ra chênh lệch bao nhiêu phần trăm."*

**ACCEPT — và đây là thay đổi có tác động lớn nhất trong cả bài.**

Bản nháp đầu chia tổng chi phí cho 140.000 ca vào. Sai. Đã đổi mẫu số sang 95.284 job hoàn thành. Cost/Job
đi từ 0,0427 $ lên **0,0627 $** — mẫu số sai làm mô hình trông rẻ hơn thực tế **31,9%**. Đã thêm hẳn hai dòng
`B100` và `B101` trong Tab 1 để con số sai và mức sai luôn hiển thị bên cạnh con số đúng, thay vì chỉ sửa
âm thầm.

Đi kèm là một quyết định về **định nghĩa job** mà bản nháp đầu làm sai: nếu chỉ tính ca AI tự đóng thì 26%
lưu lượng khiếu nại bị coi là "job hỏng", trong khi hồ sơ điều tra chính là thứ ví bỏ tiền ra mua. Đã đổi
sang định nghĩa hai đường — contained và hồ sơ duyệt lần đầu — và cả hai đều là state transition đếm tự động
được, nối thẳng về NSM đã chốt ở Day 23.

### 3 · Soát lại phép tính token

| # | Điểm phản biện | Quyết định | Đã làm gì |
|---|---|:--:|---|
| 3.1 | `AGENT_MAX_STEPS` trong mô hình đang lấy giá trị 6 từ lượt chạy 22/08, nhưng lượt chạy hiện hành đặt **8** | **ACCEPT** | Nâng số lượt gọi LLM của lớp B từ 14 lên 16. Cost/Job tăng từ 0,0614 $ lên 0,0627 $. |
| 3.2 | Chưa định lượng phần tiết kiệm nhờ prompt caching | **ACCEPT** | Thêm dòng `B52`/`B53` tính chi phí LLM trong kịch bản không cache: caching đang cắt **58,2%** chi phí LLM. Thêm luôn dòng "bỏ prompt caching" vào bảng độ nhạy — nó làm bội số rơi xuống 2,48×. |
| 3.3 | Batch API giảm 50%, có dùng được không? | **REJECT cho v1** | Lớp B là hội thoại có khách đang chờ ở đầu bên kia, latency p50 đo được 6,17 giây. Batch (độ trễ tính bằng giờ) phá vỡ trải nghiệm. Đúng là có một nhánh dùng được — hồ sơ "chạm ngân hàng" với SLA tra soát tính bằng ngày — nhưng đưa nó vào mô hình cơ sở là tự thưởng cho mình một khoản tiết kiệm chưa xây. Ghi vào danh sách đòn bẩy, không ghi vào bảng giá. |

### 4 · Biến động giá

| # | Điểm phản biện | Quyết định | Đã làm gì |
|---|---|:--:|---|
| 4.1 | Giá nào đang là giá khuyến mại? | **ACCEPT** | Mở lại cả hai trang giá ngày 27/08/2026. Phát hiện tài liệu Lab đã cũ ở một điểm: Sonnet 5 mức 2/10 $ nay là giá chuẩn, đợt tăng lên 3/15 $ từ 01/09/2026 **sẽ không diễn ra**. Ghi vào tab 6 kèm ngày kiểm tra. |
| 4.2 | DeepSeek có cấu trúc **peak / off-peak** gấp đôi, và khung peak của họ (01–04h và 06–10h UTC) trùng gần khít giờ hành chính Việt Nam — nơi toàn bộ lưu lượng CSKH nằm | **ACCEPT** | Đây là phát hiện tôi đã bỏ sót hoàn toàn ở bản nháp. Thêm ô tỷ lệ peak (65%) và tính giá hoà thay vì dùng giá off-peak. Thêm kịch bản 100% peak vào bảng độ nhạy. |
| 4.3 | Tính lại Cost/Job ở kịch bản đổi sang model tuyến đầu | **ACCEPT** | Thêm dòng "đổi sang Claude Haiku 4.5": bội số rơi từ 3,68× xuống **1,97×**, GM còn 49,19%. Kết luận đưa lên One-Pager: chọn model không phải chi tiết kỹ thuật, nó là biến sống còn. |

### 5 · Độ nhạy breakeven

**ACCEPT toàn bộ**, nhưng phải sửa cách giải mà bản nháp làm sai.

Bản nháp giải breakeven bằng một "giá bình quân hoà" cố định, rồi cho tỷ lệ hoàn thành chạy. Sai, vì hai
đường job có đơn giá lệch nhau 6,3 lần — hạ containment lớp A làm mix nghiêng về hồ sơ và **đẩy giá bình
quân lên**, nên công thức tuyến tính cho kết quả mâu thuẫn với bảng quét. Đã bỏ cách đó và giải riêng từng
biến, giữ biến kia cố định:

- Breakeven theo **tỷ lệ hồ sơ duyệt-lần-đầu** (giữ containment 80%): **≥ 46,67%** cho ngưỡng 3×, **≥ 28,89%** cho GM 60%.
- Breakeven theo **containment lớp A** (giữ hồ sơ 71%): chỉ **15,55%** — thấp đến mức gần như không ràng buộc.

Từ đó rút ra kết luận quan trọng nhất của cả bài: **biến quyết định sống chết là đường hồ sơ, không phải
containment.** Đã dựng thêm ma trận GM hai chiều ở Tab 2 để thấy điều đó bằng màu: đi ngang thì ô đổi màu,
đi dọc thì gần như không.

Cũng trong mục này, một quan sát mà bản nháp không nhìn ra: **hai ngưỡng của Lab không độc lập.** Giá bán
chia Cost/Job đúng bằng Doanh thu chia COGS, tức bằng 1/(1−GM). Nên "≥ 3×" chính là "GM ≥ 66,67%", chặt hơn
ngưỡng GM 60%. Ràng buộc thật của mô hình này là 3×, và One-Pager nói thẳng điều đó thay vì báo hai ngưỡng
như thể chúng là hai phép thử riêng.

### 6 · Con số nào giết mô hình nếu sai gấp đôi

**Câu trả lời của AI:** chi phí token.
**Quyết định: REJECT.**

Trong mô hình này token chỉ chiếm 32,6% COGS, và LLM sai gấp đôi vẫn giữ được GM 63,4%. Con số thật sự
nguy hiểm là **lao động người**: QA nội bộ cộng CSM chiếm **54% COGS**, sai gấp đôi là bội số rơi xuống
2,54× và trượt ngưỡng. Nó cũng là con số ít bằng chứng nhất — mới suy ra từ giai đoạn demo, chưa từng đo ở
tải 140.000 ca/tháng.

Điểm đáng nói: câu trả lời sai của AI phản ánh đúng linh cảm mặc định của ngành ("chi phí AI là chi phí
token"). Với sản phẩm chạy model rẻ ở thị trường lao động rẻ, linh cảm đó sai theo cả hai chiều — token rẻ
hơn ta tưởng, và giờ người đắt hơn ta tưởng khi cộng dồn.

### Một điểm AI không nêu mà tôi tự thêm

Prompt không hỏi về **biến thể HITL**, nhưng đây là chỗ Cost/Job có thể sai vài lần. Đã mô phỏng hẳn Biến
thể B trong Tab 2: nếu ta nhận trách nhiệm giao kết quả cuối, GM đi từ +72,9% xuống **−61,3%** và cần tỷ lệ
hoàn thành 94,1%. Con số đó về sau trở thành lập luận chính cho việc không bán Outcome ở Tab 3 — mạnh hơn
mọi lập luận định tính mà tôi định viết.

---

## §4.7.5 — One-Pager Defensibility Check

Chạy trên bản nháp One-Pager, trước khi xuất PDF.

| # | Điểm phản biện | Quyết định | Đã làm gì |
|---|---|:--:|---|
| 1 | *"Con số nào trong tài liệu mà bạn không nói được vì sao là con số đó?"* — chỉ ra ba chỗ: mix 62/26/12, containment 80%, đơn giá QA 3,30 $/giờ | **ACCEPT** | Không bịa lý do cho ba con số đó. Thay vào đó gắn nhãn "ước tính / chưa đo" ngay tại ô trong Excel, đưa cả ba vào mục "Giới hạn đã biết" của README, và đưa hai trong ba vào KPI tháng 1. Thành thật về khoảng trống rẻ hơn là để người chấm tự phát hiện. |
| 2 | *"Claim nào bạn sẽ bị vặn đầu tiên?"* — GM 72,9% so với benchmark AI-native 52–53% | **ACCEPT** | Thêm hẳn một ô giải trình ba lý do kiểm chứng được (model rẻ · lao động VN rẻ · Biến thể A đẩy chi phí escalate sang phía ví), kèm câu chốt "không phải ta giỏi hơn thị trường". Đặt ngay cạnh bảng độ nhạy để người đọc tự thấy GM sập khi bỏ bất kỳ lý do nào. |
| 3 | *"Một founder đối thủ có viết được đúng one-pager này với số của họ không?"* | **ACCEPT** | Có, ở bản nháp thì được — vì nó toàn số đẹp và câu chữ chung chung. Đã đổi trục: đưa phán quyết "chưa được ký hợp đồng" lên ngay đầu trang, gắn nó vào một con số đo được có provenance (1,03% so với ngưỡng 46,67%), và trỏ thẳng vào nguyên nhân kỹ thuật cụ thể. Không đối thủ nào chép được đoạn đó. |
| 4 | *"Cost/Job, giá, GM và breakeven có khớp nhau về số học không?"* | **ACCEPT** | Bắt được một lỗi thật: bản nháp ghi breakeven 44,46% trong khi Excel ra 46,67%, do bản nháp viết trước khi sửa `AGENT_MAX_STEPS` từ 6 lên 8. Đã đồng bộ lại toàn bộ và thêm hàng "Truy vết" ở chân One-Pager, ánh xạ từng con số về đúng một ô. |
| 5 | *"Kênh có suy ra từ ARPU và pain moment, hay được chọn độc lập?"* | **PARTIAL** | Kênh suy ra từ số học (ngân sách CAC dư 8,59×) — chỗ này chặt. Nhưng bản nháp chưa nối kênh với pain moment. Đã thêm đoạn về **điểm nhúng**: pain moment xảy ra trong công cụ CSKH của ví, nên sản phẩm phải là connector cộng panel chứ không phải web app riêng, và chính điều đó là thứ phí nền 130tr đổi lấy. Ghi thêm cái giá phải trả khi nhúng, lấy Intercom bỏ doanh thu seat làm đối chiếu. |
| 6 | *"Một sửa đổi làm tài liệu này chắc chắn hơn gấp 10 lần"* — đề xuất: đưa con số eval đo được lên ngay đầu trang thay vì giấu ở mục Evidence | **ACCEPT** | Đã làm. Khối "ĐỌC TRƯỚC" ở đầu One-Pager giờ nói thẳng: ngưỡng 46,67%, đo được 1,03%, kết luận chưa được ký. Đây cũng là sửa đổi khiến tài liệu tự mâu thuẫn ít nhất — trước đó phần Pricing khoe GM 72,9% còn phần Evidence thú nhận eval chưa đạt, mà không chỗ nào nối hai điều đó lại. |

---

## Ghi chú về nguồn dữ liệu — một lần phải làm lại

Trong lúc dựng mô hình, thư mục `eval/results/` của P-121 được cập nhật (26–27/08/2026) và bổ sung một
`README.md` nói rõ **file nào tin được, file nào không**. Toàn bộ số eval tôi dùng ban đầu — lượt 22/08 với
`hard_pass_rate` 0,9397 — bị chính tài liệu đó đánh dấu là **không so sánh được**: lượt ấy lưu nhãn hiển thị
thay vì tên tool, nên `create_ticket` và `lock_wallet` **vô hình** với bộ chấm; con số "0/47" tôi trích ban
đầu là hiện vật của phép đo, không phải hành vi của agent.

Đã thay toàn bộ bằng lượt **27/08 sau-seed**, là lượt duy nhất có provenance, có tên tool thật, và chạy trên
môi trường đã seed đủ. Hai lượt độc lập cùng cho `missed_expected_ticket = 96/97`, nên kết luận về đường hồ
sơ vẫn đứng — nhưng nó đứng trên bằng chứng đúng, chứ không phải trên bằng chứng may mà trùng.

Đây là lý do tab 6 có riêng một mục "Nguồn nội bộ" ghi ngày và cảnh báo cho từng số lấy từ sản phẩm, và là
lý do câu chốt của bài viết là: một mô hình không ghi ngày là một mô hình không tin được — và một con số
không có provenance thì không đủ tư cách làm cơ sở tính tiền.

---

## Vòng 2 — chuyển sang template chính chủ của Lab

Sau khi tải được `Day25-AI-Product-GTM-Monetization-Model.xlsx` và
`Day25-AI-Product-GTM-One-Pager-Template.docx`, tôi bỏ hai file tự dựng và làm lại trên đúng template.
Mọi con số nêu ở phần trên là của bản dựng đầu; bản nộp cuối dùng mô hình của template. Ghi lại đây để
người đọc không bị lệch giữa hai bộ số.

**Vì sao đổi.** Template là công cụ chấm. Nó có cấu trúc riêng — một loại job, một tỷ lệ containment, một
công thức breakeven `R ≥ (v+q+e) / (P×(1−GM)+e)` — và người chấm sẽ tìm từng ô ở đúng chỗ. Tự dựng một
workbook đẹp hơn nhưng khác chỗ là bắt người chấm đi tìm.

**Cái phải nhượng bộ, và cái không.** Template chỉ có một bộ tham số token cho "một hội thoại", trong khi
chi phí thật phải tính riêng ba lớp ca (A 8 lượt gọi · B 16 · C 3). Tôi điền bình quân gia quyền để công
thức gốc chạy đúng, rồi ghi khoảng lệch ra khối mở rộng: hàm chi phí **lồi** theo (số lượt × token) nên
bình quân của tích không bằng tích của bình quân, và con số template hụt **9,16%** so với tính riêng từng
lớp (1.770,74 $ so với 1.949,20 $). Tính đúng từng lớp thì Cost/Job lên 0,0625 $ và bội số còn 3,69× —
vẫn qua ngưỡng, nên kết luận không đổi. Giấu khoảng lệch này thì dễ; ghi ra thì đúng.

Tương tự, template không có ô cho nhóm chi phí phục vụ khách khác (chạy lại eval, CSM, compliance, bảo
trì prompt). Tôi gộp vào ô Infra và tách chi tiết ở khối mở rộng ③ của `1_Cost_Job`, thay vì bỏ chúng đi
cho gọn.

**Ba con số đổi theo mô hình template:**

| | Bản tự dựng | Bản template |
|---|---:|---:|
| Cost/Job | 0,0627 $ | **0,0607 $** |
| Gross Margin · bội số | 72,86% · 3,68× | **73,73% · 3,81×** |
| Breakeven đường hồ sơ (ngưỡng 3×) | 46,67% | **43,26%** |

Phán quyết không đổi: đo được 1,03% so với ngưỡng 43,26% → chưa được ký hợp đồng theo bảng giá này.

**Một phát hiện chỉ xuất hiện khi dùng template.** Ô `B19` của template hỏi "giá bán ($/job)" — một con số
duy nhất, trong khi mô hình của tôi là Hybrid. Buộc phải quy về một con số làm lộ ra điều mà bản tự dựng
giấu mất: tách riêng dòng usage ra khỏi phí nền thì bội số chỉ còn **2,94×**, trượt ngưỡng 3×. Tức phí nền
không phải khoản phụ thu cho tiện — nó là thứ kéo mô hình qua ngưỡng. Ràng buộc của template ép ra một
insight mà cấu trúc tự do của tôi che mất.

---

## Bài test người lạ — vì sao không có số

Template có ô "Số câu người đọc phải hỏi lại". Bài này làm cá nhân nên không có nhóm khác để đưa đọc, và
tôi không điền một con số bịa vào đó: đây là ô ghi kết quả một phép thử, viết ra rằng đã có người đọc
trong khi không có ai cả thì nó là số liệu giả, không phải cách trình bày.

Thay vào đó tôi ghi rõ **"tự kiểm, chưa test với người ngoài"** và liệt kê thật những chỗ vấp khi đọc lại
tài liệu như một người chưa biết gì:

1. **Dễ nhầm giá sàn với giá bán.** Bảng số có ba mức (Cost/Job 0,0607 · giá sàn 0,1820 · giá bán 0,2309)
   và mắt người đọc bám vào con số lớn nhất. Đã sửa: gắn nhãn kết luận ngay cạnh dòng giá bán.
2. **Vì sao Gross Margin 73,7% mà vẫn kết luận chưa được ký.** Ở bản nháp, phần Pricing khoe biên đẹp còn
   phần Evidence thú nhận eval chưa đạt, mà không chỗ nào nối hai điều đó lại — người đọc phải tự ghép.
   Đã sửa: đưa phán quyết lên ngay đầu One-Pager và nói rõ đó là hai trạng thái khác nhau (điểm vận hành
   mục tiêu so với mức đo được).

Ô số thật sẽ điền sau khi có người ngoài đọc. Thành thật về một ô trống có deadline được điểm cao hơn một
ô điền số không có thật — và đó cũng đúng là nguyên tắc mà chính bài Lab này dạy ở phần Evidence Pack.
