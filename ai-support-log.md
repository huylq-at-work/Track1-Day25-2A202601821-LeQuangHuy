# AI Support Log — Track 1 · Day 25

**Lê Quang Huy · MHV 2A202601821**
Sản phẩm: WalletCare / FIN-05 — AI Agent CSKH ví điện tử & xử lý khiếu nại giao dịch (nhóm T121, repo `P-121`)
Công cụ AI đã dùng: Claude Opus 5 (Claude Code)

---

## 1. Phần không có AI — của riêng tôi

- **Chọn sản phẩm và chọn phạm vi.** Day 25 nối tiếp Day 23 và Day 24 trên cùng FIN-05, thay vì lấy một
  case giả định cho dễ ra số đẹp.
- **Định nghĩa "1 job" theo hai đường — contained và hồ sơ duyệt lần đầu.** Đây là quyết định lõi của cả
  bài, và nó đến từ việc tôi đối chiếu với NSM đã chốt ở Day 23, không đến từ gợi ý của AI (xem mục 3a).
- **Chọn Biến thể A và giải thích vì sao đó không phải lựa chọn tiết kiệm mà là ràng buộc pháp lý**:
  người duyệt là người của ví, ta không được phép nhận việc đó.
- **Chốt Value Metric là Hybrid, chốt kênh là Sales-Led, chốt Pain Moment và điểm nhúng.**
- **Quyết định đưa phán quyết "chưa được ký hợp đồng" lên đầu One-Pager** thay vì để bài nộp trông đẹp.
- **Quyết định đặt mục tiêu ký 0 hợp đồng trong tháng 1** của kế hoạch 90 ngày.
- **Bác bỏ ba khuyến nghị của AI** — xem mục 3.

---

## 2. AI đã giúp tôi ở đâu

- **Đọc và đối chiếu tài liệu.** AI đọc `FIN05-Brief.md`, `src/core/config.py`, thư mục `eval/results/` và
  các bài Day 21–24 để lấy ngữ cảnh và trích ra những tham số thật (`AGENT_MAX_STEPS`, `agent_token_budget`,
  `agent_history_turns`, đơn giá metering trong mã).
- **Kiểm tra giá API tại nguồn.** AI mở trang giá DeepSeek và Anthropic ngày 27/08/2026 và đối chiếu với
  bảng §3.5 của tài liệu Lab — nhờ đó phát hiện tài liệu Lab đã cũ ở dòng Sonnet 5.
- **Dựng file Excel bằng công thức sống** thay vì gõ số cứng, để mọi ô đều truy ngược được.
- **Đóng vai phản biện theo prompt §4.7.1 và §4.7.5.** Toàn bộ điểm phản biện và quyết định
  accept / reject / partial của tôi được ghi ở [`docs/critique-log.md`](docs/critique-log.md).
- **Soát nhất quán số học** giữa Excel và One-Pager, phát hiện một chỗ lệch thật (breakeven 44,46% so với
  46,67%, do bản nháp viết trước khi tôi sửa `AGENT_MAX_STEPS`).

**Không dùng AI cho:** định nghĩa job, chọn Value Metric, chọn kênh, viết Pain Moment, chọn các mốc KPI
tháng 1, và chọn cách trình bày phán quyết.

---

## 3. AI sai, hời hợt hoặc thiếu ở đâu

**a) AI định nghĩa "1 job" quá hẹp và suýt làm hỏng cả mô hình.**
Bản đầu AI đề xuất job = "1 ca AI tự giải quyết xong", theo đúng khuôn Intercom Fin. Với FIN-05 thì đó là
định nghĩa sai: 26% lưu lượng là khiếu nại giao dịch, HITL bắt buộc, nên chúng **không bao giờ** được AI tự
đóng — định nghĩa đó biến toàn bộ phần giá trị nhất của sản phẩm thành "job hỏng". Tôi đổi sang định nghĩa
hai đường, lấy đúng cặp sự kiện đã chốt ở Day 23. Nếu giữ định nghĩa của AI, Cost/Job sẽ bị thổi lên và
kết luận về Value Metric sẽ ngược lại.

**b) AI trả lời sai câu "con số nào giết mô hình".**
AI nói: chi phí token. Sai. Trong mô hình này token chỉ chiếm 32,6% COGS và LLM sai gấp đôi vẫn giữ GM
63,4%; còn lao động người chiếm 54% COGS và sai gấp đôi là trượt ngưỡng 3×. Đây là linh cảm mặc định của
ngành ("chi phí AI là chi phí token") áp lên một sản phẩm chạy model rẻ ở thị trường lao động rẻ — nơi linh
cảm đó sai theo cả hai chiều.

**c) AI bỏ sót cấu trúc giá peak / off-peak của DeepSeek.**
Bản nháp đầu dùng giá off-peak cho toàn bộ lưu lượng. Chỉ khi đọc kỹ trang giá mới thấy khung peak
01–04h và 06–10h UTC quy ra giờ Việt Nam là 08–11h và 13–17h — trùng gần khít giờ hành chính, tức trùng
đúng chỗ toàn bộ lưu lượng CSKH nằm. Đã thêm ô tỷ lệ peak và kịch bản 100% peak.

**d) AI dùng đơn giá lao động 9 $/giờ theo ví dụ mẫu trong tài liệu Lab.**
Tôi bác. Đó là giá offshore chung chung, không phải giá Việt Nam. Thay bằng 3,30 $/giờ, tính ngược từ mức
fully-loaded 15tr ₫/tháng chia 176 giờ — con số mà chính ví cũng kiểm chứng được từ bảng lương của họ.

**e) AI giải breakeven bằng một công thức tuyến tính cho ra kết quả mâu thuẫn với bảng quét của chính nó.**
Nguyên nhân: nó dùng một "giá bình quân hoà" cố định, trong khi hai đường job có đơn giá lệch 6,3 lần nên
mix thay đổi thì giá bình quân cũng thay đổi. Tôi bỏ cách đó, giải riêng từng biến và giữ biến kia cố định.
Nhờ vậy mới thấy điều quan trọng nhất của cả bài: biến quyết định là **đường hồ sơ**, không phải containment.

**f) AI đề xuất neo giá trần theo quy tắc "50–70% lương vị trí bị thay".**
Tôi bác. Quy tắc đó chỉ đúng khi ta **thay** một người. FIN-05 không thay CSKH — HITL là bắt buộc, ví vẫn
trả đủ lương cho CSKH và cho cấp duyệt; ta chỉ rút ngắn thời gian mỗi ca. Neo đúng là 10–25% giá trị tạo ra,
và ta nằm ở nửa dưới của khoảng đó vì đang ở giai đoạn land.

**g) AI gợi ý nâng giá để ngưỡng 3× "thoáng hơn cho đẹp".**
Tôi bác. Bảng giá đã nằm trong vùng sàn–trần và ở mức 17,6% giá trị tạo ra; nâng giá chỉ để bội số nhìn
thoải mái là làm đúng cái việc mà chính tài liệu Lab cấm — sửa giá thay vì sửa mô hình.

**h) AI dùng dữ liệu eval đã bị chính repo đánh dấu là không tin được.**
Đây là lỗi nghiêm trọng nhất trong phiên. Bản dựng đầu lấy số từ lượt chạy 22/08/2026 (`hard_pass_rate`
0,9397, "0/47 ticket"). Sau khi thư mục `eval/results/` được cập nhật ngày 26–27/08 kèm một `README.md` nói
rõ file nào tin được, hoá ra lượt đó lưu **nhãn hiển thị** thay vì tên tool, nên `create_ticket` và
`lock_wallet` vô hình với bộ chấm — con số tôi trích là hiện vật của phép đo chứ không phải hành vi của
agent. Đã thay toàn bộ bằng lượt 27/08 sau-seed, là lượt duy nhất có provenance. May là hai lượt độc lập
cùng cho `missed_expected_ticket = 96/97` nên kết luận không đổi; nhưng nếu chúng lệch nhau thì cả bài đã
sai. Bài học này quan trọng đến mức tôi đưa hẳn nó vào tab 6 và vào README như một kết luận của bài, chứ
không giấu trong log.

---

## 4. Điều tôi rút ra

Mô hình tài chính không có nhiệm vụ làm sản phẩm trông tốt. Nhiệm vụ của nó là chỉ ra sản phẩm gãy ở đâu,
sớm hơn thị trường một nhịp. Bài này cho ra một Gross Margin 72,9% nghe rất đẹp và một phán quyết "chưa
được phép bán" nghe rất xấu — và phán quyết mới là phần đáng giá. Phát hiện ở tháng thứ nhất rằng đường hồ
sơ đang ở 1,03% thay vì 46,67% rẻ hơn rất nhiều so với phát hiện điều đó ở tháng thứ ba, sau khi đã ký.
