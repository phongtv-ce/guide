# Hướng dẫn sử dụng Scrum với Kanban

Tài liệu này mô tả cách vận hành một board Kanban 11 cột trong khuôn khổ Scrum: ý nghĩa từng cột, quy định khi tạo thẻ và chuyển trạng thái, và các nguyên tắc để làm việc hiệu quả.

## Mục lục

1. [Mục tiêu và phạm vi](#1-mục-tiêu-và-phạm-vi)
2. [Tổng quan Scrum + Kanban](#2-tổng-quan-scrum--kanban)
3. [Giải thích các cột](#3-giải-thích-các-cột)
4. [Quy định định nghĩa và chuyển trạng thái](#4-quy-định-định-nghĩa-và-chuyển-trạng-thái)
5. [WIP limit và chính sách kéo](#5-wip-limit-và-chính-sách-kéo-pull)
6. [Nhịp Scrum trên board](#6-nhịp-scrum-trên-board)
7. [Nguyên tắc làm việc hiệu quả](#7-nguyên-tắc-làm-việc-hiệu-quả)
8. [Chỉ số gợi ý](#8-chỉ-số-gợi-ý)
9. [Lỗi thường gặp](#9-lỗi-thường-gặp-anti-patterns)
10. [Checklist nhanh](#10-checklist-nhanh)

---

## 1. Mục tiêu và phạm vi

**Mục tiêu**

- Giúp cả nhóm hiểu chung một cách làm việc: cùng nhìn vào board là biết công việc đang ở đâu, ai đang giữ, bước tiếp theo là gì.
- Thống nhất điều kiện để một thẻ (card) được phép chuyển từ cột này sang cột khác, tránh tranh cãi "xong" nghĩa là gì.
- Giảm thời gian chờ, giảm việc dang dở, giao giá trị đều đặn sau mỗi sprint.

**Phạm vi**

- Áp dụng cho nhóm nhỏ hoặc cá nhân làm phát triển sản phẩm/phần mềm theo Scrum.
- Nhóm gồm 3–5 người với hai vai trò chính thức là **Dev** và **Tester**. Nhóm không có Product Owner và Scrum Master riêng; trách nhiệm của hai vai trò này được giao lại cho *Trưởng nhóm* và *Điều phối viên* (xem mục 2).
- Scrum quyết định *nhịp và cam kết* (sprint, sự kiện, Sprint Goal). Kanban quyết định *cách hiển thị và điều tiết luồng công việc* (cột, WIP limit, pull).
- Các con số gợi ý (WIP limit, số ngày quá hạn...) là điểm khởi đầu. Nhóm nên điều chỉnh sau các buổi Retrospective.

---

## 2. Tổng quan Scrum + Kanban

| | Scrum cung cấp | Kanban cung cấp |
|---|---|---|
| Thời gian | Sprint có độ dài cố định (1–4 tuần) | Luồng liên tục trong sprint |
| Cam kết | Sprint Goal, Sprint Backlog | Giới hạn WIP theo cột |
| Vai trò | Scrum gốc có Product Owner, Scrum Master, Developers; nhóm rút gọn còn Dev và Tester | Không quy định (dùng lại vai trò của nhóm) |
| Hiển thị | Sprint Backlog, Increment | Board, cột, thẻ, chỉ số luồng |
| Cải tiến | Sprint Retrospective | Phân tích điểm nghẽn, cycle time |

### Luồng công việc

```
Open → Product Backlog → Sprint Backlog → Today Todo → In Progress
                                                          │
   ┌──────────────────────────────────────────────────────┘
   ↓
Ready to Review → Ready to Test → Ready to Release → Released → Closed

Nhánh phụ:
  Waiting   ⇄  Today Todo / In Progress        (bị chặn bởi yếu tố bên ngoài)
  Ready to Review / Ready to Test  →  In Progress   (bị reject, cần sửa)
  Open / Product Backlog  →  Closed             (không làm, có lý do)
```

Bốn vùng của board:

| Vùng | Các cột | Ý nghĩa |
|---|---|---|
| Chuẩn bị | Open, Product Backlog, Sprint Backlog | Thu thập, làm rõ, sắp xếp ưu tiên, cam kết vào sprint |
| Sẵn sàng làm | Waiting, Today Todo | Việc đã cam kết nhưng đang bị chặn (Waiting) hoặc đã chọn cho hôm nay (Today Todo) |
| Thực thi | In Progress, Ready to Review, Ready to Test | Làm, review code, kiểm thử |
| Phát hành và đóng | Ready to Release, Released, Closed | Chờ phát hành, đã phát hành, đã hoàn tất hoặc đã hủy |

> **Lưu ý về Waiting:** Waiting không phải là một bước bắt buộc trong luồng. Đây là cột "đỗ xe" cho thẻ bị chặn bởi yếu tố bên ngoài. Thẻ có thể vào Waiting từ bất kỳ cột thực thi nào và quay lại đúng cột cũ khi được gỡ chặn.

### Vai trò và trách nhiệm

Nhóm chỉ có hai vai trò chính thức là **Dev** và **Tester**. Trách nhiệm của Product Owner và Scrum Master trong Scrum gốc được giao lại như sau:

| Vai trò / trách nhiệm | Ai đảm nhận | Nhiệm vụ chính |
|---|---|---|
| **Dev** | Các thành viên phát triển | Làm việc, review chéo (Dev khác tác giả thẻ), tự chọn thẻ vào Today Todo, deploy |
| **Tester** | Người kiểm thử | Kiểm thử theo tiêu chí chấp nhận, **nghiệm thu chất lượng** thẻ trước Ready to Release, smoke test sau phát hành |
| **Trưởng nhóm** (thay Product Owner) | Một Dev do nhóm chọn | Chốt thứ tự ưu tiên backlog, phân loại thẻ ở Open, quyết định thêm/đánh đổi việc giữa sprint, đóng thẻ (Closed) |
| **Điều phối viên** (thay Scrum Master) | Một người cố định (mặc định là Trưởng nhóm); ghi tên: `__________` | Chủ trì các sự kiện Scrum, theo dõi cột Waiting và leo thang, nhắc nhóm giữ WIP limit và DoD |

Lưu ý:

- Trưởng nhóm và Điều phối viên là trách nhiệm kèm theo, không phải vai trò riêng; một người có thể đảm nhận cả hai.
- Người viết thẻ không tự review và không tự nghiệm thu thẻ của mình. Review do Dev khác làm; nghiệm thu chất lượng do Tester làm.
- Khi nhóm không đồng thuận về ưu tiên, Trưởng nhóm quyết định.

---

## 3. Giải thích các cột

### Bảng tổng hợp

| # | Cột | Mục đích | Người sở hữu | WIP limit gợi ý |
|---|---|---|---|---|
| 1 | **Open** | Nơi tiếp nhận mọi yêu cầu, ý tưởng, bug, chưa phân loại | Ai cũng được thêm; Trưởng nhóm phân loại | Không giới hạn (nhưng dọn hằng tuần) |
| 2 | **Product Backlog** | Danh sách có thứ tự ưu tiên những việc sẽ làm cho sản phẩm | Trưởng nhóm | Không giới hạn; phần đầu phải luôn sẵn sàng |
| 3 | **Sprint Backlog** | Việc nhóm cam kết hoàn thành trong sprint hiện tại | Cả nhóm (Dev và Tester) | Theo năng lực (velocity) của sprint |
| 4 | **Waiting** | Việc đang bị chặn bởi yếu tố bên ngoài | Người giữ thẻ | Tối đa 3 thẻ |
| 5 | **Today Todo** | Việc đã chọn để làm trong hôm nay | Từng Dev | Vừa đủ cho 1 ngày làm việc |
| 6 | **In Progress** | Việc đang thực sự được làm | Người được giao | 1–2 thẻ cho mỗi người |
| 7 | **Ready to Review** | Code/sản phẩm đã xong, chờ người khác review | Dev khác (không phải tác giả) | Tối đa bằng số người review × 2 |
| 8 | **Ready to Test** | Đã qua review, chờ kiểm thử | Tester | Tối đa 3–5 thẻ |
| 9 | **Ready to Release** | Đã qua kiểm thử, sẵn sàng phát hành | Tester (nghiệm thu) + Trưởng nhóm | Không để tồn quá 1 chu kỳ phát hành |
| 10 | **Released** | Đã phát hành lên môi trường thật | Dev phát hành | Không giới hạn; chờ xác nhận |
| 11 | **Closed** | Đã hoàn tất, hoặc bị hủy với lý do rõ ràng | Trưởng nhóm | Không giới hạn; có thể lưu trữ định kỳ |

### Chi tiết từng cột

#### 1. Open

- **Là gì:** hộp thư đến của board. Mọi yêu cầu mới, bug, ý tưởng, câu hỏi đều bắt đầu ở đây.
- **Vào cột khi:** bất kỳ ai tạo thẻ mới.
- **Yêu cầu tối thiểu:** một tiêu đề đủ hiểu và một đoạn mô tả ngắn (vấn đề là gì, ai gặp phải).
- **Ra khỏi cột khi:** Trưởng nhóm xem xét và quyết định: đưa vào Product Backlog, hoặc đóng (trùng lặp, không làm, ngoài phạm vi) ở cột Closed kèm lý do.
- **Lưu ý:** thẻ ở Open *chưa* có cam kết nào. Không ước lượng, không giao việc ở đây.

#### 2. Product Backlog

- **Là gì:** danh sách duy nhất, được sắp xếp theo thứ tự ưu tiên, của những việc sản phẩm cần. Thẻ ở trên cùng quan trọng nhất và phải rõ nhất.
- **Vào cột khi:** Trưởng nhóm đã xem xét thẻ ở Open và thấy đáng làm.
- **Ra khỏi cột khi:** thẻ đạt *Definition of Ready* (mục 4.2) và được chọn trong Sprint Planning.
- **Lưu ý:** thẻ ở đáy có thể còn thô. Refinement (mục 6) làm mịn dần phần đầu backlog, khoảng 1–2 sprint tới.

#### 3. Sprint Backlog

- **Là gì:** cam kết của nhóm cho sprint hiện tại, gồm Sprint Goal và các thẻ được chọn.
- **Vào cột khi:** được chọn trong Sprint Planning và đạt Definition of Ready.
- **Ra khỏi cột khi:** Dev kéo thẻ sang Today Todo (hoặc trực tiếp sang In Progress nếu bắt đầu ngay).
- **Lưu ý:** không thêm thẻ vào cột này giữa sprint trừ khi có thỏa thuận với Trưởng nhóm và bỏ bớt thẻ có giá trị tương đương.

#### 4. Waiting

- **Là gì:** nơi để những việc đã cam kết nhưng không thể tiến tiếp vì phụ thuộc bên ngoài (chờ phản hồi khách hàng, chờ API của nhóm khác, chờ quyết định, chờ môi trường).
- **Vào cột khi:** thẻ bị chặn và Dev *không thể tự gỡ* trong ngày.
- **Bắt buộc ghi trên thẻ:** (1) lý do bị chặn, (2) ai chịu trách nhiệm gỡ chặn, (3) ngày dự kiến có kết quả, (4) cột trước đó để quay lại.
- **Ra khỏi cột khi:** chặn được gỡ. Thẻ quay lại Today Todo hoặc đúng cột trước đó.
- **Lưu ý:** thẻ chờ quá **2 ngày làm việc** phải được nêu ở Daily và có hành động leo thang. Việc "chờ" là việc của Điều phối viên để gỡ, không phải để quên.

#### 5. Today Todo

- **Là gì:** kế hoạch của từng người cho hôm nay, chọn từ Sprint Backlog.
- **Vào cột khi:** trong Daily hoặc đầu ngày, Dev chọn thẻ ưu tiên cao nhất còn lại trong Sprint Backlog.
- **Ra khỏi cột khi:** bắt đầu làm (sang In Progress), hoặc hết ngày mà chưa làm thì quay lại Sprint Backlog để chọn lại vào hôm sau.
- **Lưu ý:** chỉ chọn lượng việc thực tế làm được trong ngày (kể cả review giúp đồng đội). Không biến cột này thành backlog thứ hai.

#### 6. In Progress

- **Là gì:** những việc đang được làm ngay lúc này.
- **Vào cột khi:** Dev bắt đầu làm, có gán tên người làm.
- **Ra khỏi cột khi:** đạt DoD của cổng "Ready to Review" (mục 4.3), hoặc bị chặn (sang Waiting).
- **Lưu ý:** WIP tối đa 1–2 thẻ mỗi người. Nếu bị chặn, đừng bắt đầu thẻ mới cho đầy WIP; hãy hỗ trợ review hoặc gỡ chặn.

#### 7. Ready to Review

- **Là gì:** việc đã làm xong phần của mình, chờ đồng đội xem xét (code review, design review, doc review).
- **Vào cột khi:** đạt DoD cổng Review; đã mở Pull Request/yêu cầu review và gắn link vào thẻ.
- **Ra khỏi cột khi:** Dev review phê duyệt → Ready to Test; Dev review yêu cầu sửa → quay lại In Progress kèm ghi chú.
- **Lưu ý:** review là ưu tiên cao hơn bắt đầu việc mới. Mục tiêu phản hồi trong **1 ngày làm việc**.

#### 8. Ready to Test

- **Là gì:** thay đổi đã qua review, đã được tích hợp vào môi trường kiểm thử, chờ kiểm thử theo tiêu chí chấp nhận.
- **Vào cột khi:** đạt DoD cổng Test; đã deploy lên môi trường test/staging.
- **Ra khỏi cột khi:** test đạt → Ready to Release; test lỗi → quay lại In Progress kèm mô tả lỗi và cách tái hiện.
- **Lưu ý:** người kiểm thử nên khác người viết code khi có thể. Lỗi tìm thấy ghi ngay trên thẻ gốc nếu là lỗi của chính thay đổi đó; lỗi không liên quan tạo thẻ mới ở Open.

#### 9. Ready to Release

- **Là gì:** việc đã đạt mọi tiêu chí chất lượng, chỉ chờ quyết định/lịch phát hành.
- **Vào cột khi:** đạt DoD cổng Release; Tester đã nghiệm thu theo tiêu chí chấp nhận.
- **Ra khỏi cột khi:** được phát hành lên môi trường thật → Released; nếu phát hành thất bại/rollback → quay lại In Progress hoặc Ready to Test tùy nguyên nhân.
- **Lưu ý:** không để thẻ tồn ở đây lâu; đó là giá trị chưa đến tay người dùng.

#### 10. Released

- **Là gì:** việc đã có mặt trên môi trường thật.
- **Vào cột khi:** đã deploy thành công và qua smoke test.
- **Ra khỏi cột khi:** hết thời gian theo dõi sau phát hành (ví dụ 1–3 ngày) và Tester xác nhận không còn lỗi, Trưởng nhóm xác nhận đạt mục tiêu → Closed; nếu phát sinh lỗi nghiêm trọng → mở thẻ bug mới ở Open (hoặc kéo ngược nếu cần khắc phục khẩn).
- **Lưu ý:** phát hành chưa có nghĩa là hoàn thành. Cần xác nhận giá trị đã đến với người dùng.

#### 11. Closed

- **Là gì:** kết thúc vòng đời của thẻ. Có hai loại: **Hoàn thành** (đã Released và xác nhận) và **Không làm** (hủy, trùng lặp, hết cần, ngoài phạm vi).
- **Vào cột khi:** Trưởng nhóm xác nhận. Với thẻ *Không làm*, bắt buộc ghi lý do đóng.
- **Ra khỏi cột khi:** chỉ mở lại bằng cách tạo thẻ mới ở Open và liên kết thẻ cũ. Không kéo thẻ Closed ngược lại board.
- **Lưu ý:** lưu trữ (archive) thẻ Closed định kỳ (ví dụ cuối mỗi sprint) để board gọn.

---

## 4. Quy định định nghĩa và chuyển trạng thái

### 4.1. Quy tắc chung cho mọi thẻ

Mỗi thẻ cần có (mức độ bắt buộc tăng dần theo cột, xem 4.2):

| Trường | Yêu cầu |
|---|---|
| Tiêu đề | Ngắn, bắt đầu bằng động từ, đủ hiểu khi đứng riêng (ví dụ: "Thêm phân trang cho danh sách đơn hàng") |
| Mô tả | Bối cảnh, vấn đề, kết quả mong muốn |
| Loại | Story / Bug / Task / Spike (nhãn) |
| Tiêu chí chấp nhận | Danh sách kiểm tra có thể xác minh được (từ Product Backlog trở đi) |
| Ước lượng | Story point hoặc giờ (từ Sprint Backlog trở đi) |
| Người phụ trách | Có tên một người (từ In Progress trở đi) |
| Liên kết | Ticket liên quan, PR, tài liệu, môi trường test |
| Nhãn / mức ưu tiên | Theo thỏa thuận của nhóm |

Nguyên tắc chung khi chuyển trạng thái:

1. **Người kéo thẻ chịu trách nhiệm xác minh điều kiện vào cột.** Không kéo thẻ khi chưa đạt điều kiện.
2. **Kéo (pull), không đẩy (push).** Cột sau chủ động kéo khi có năng lực, thay vì cột trước đẩy sang.
3. **Mỗi lần chuyển ngược phải có ghi chú lý do** trên thẻ.
4. **Đi tuần tự theo thứ tự cột.** Chuyển ngược, bỏ qua cột hoặc dùng luồng rút gọn phải ghi lý do trên thẻ (xem 4.4).
5. **Cập nhật board ngay khi trạng thái đổi**, không chờ đến Daily.

### 4.2. Definition of Ready (DoR) – điều kiện vào Sprint Backlog

Thẻ chỉ được đưa vào Sprint Backlog khi:

- [ ] Có mô tả rõ ràng, cả nhóm hiểu giá trị và mục tiêu
- [ ] Có tiêu chí chấp nhận cụ thể, kiểm chứng được
- [ ] Đã được ước lượng bởi nhóm
- [ ] Đủ nhỏ để hoàn thành trong một sprint (nếu quá lớn, tách nhỏ)
- [ ] Các phụ thuộc đã biết và không chặn việc bắt đầu (hoặc đã có kế hoạch xử lý)
- [ ] Trưởng nhóm đã xác nhận mức ưu tiên
- [ ] Nếu cần thiết kế/UX/tài liệu tham khảo thì đã có

### 4.3. Definition of Done (DoD) theo từng cổng

DoD chung của nhóm được kiểm tra dần qua từng cổng chuyển cột:

| Chuyển sang | Điều kiện phải đạt (checklist) |
|---|---|
| **Ready to Review** | Code/nội dung hoàn thành theo tiêu chí chấp nhận · Tự kiểm tra và chạy được ở máy local · Unit test cần thiết đã viết và đạt · Không còn lỗi lint/build · Đã mở PR, mô tả thay đổi, gắn link vào thẻ |
| **Ready to Test** | Review đã được phê duyệt, mọi góp ý đã xử lý · Đã merge vào nhánh tích hợp · CI xanh · Đã deploy lên môi trường test · Ghi chú cách kiểm thử trên thẻ |
| **Ready to Release** | Đã kiểm thử đạt toàn bộ tiêu chí chấp nhận · Không còn bug mức chặn/nghiêm trọng · Kiểm thử hồi quy liên quan đạt · Tài liệu, changelog, ghi chú phát hành đã cập nhật · Tester nghiệm thu |
| **Released** | Đã deploy thành công lên môi trường thật · Smoke test đạt · Giám sát/cảnh báo không có bất thường · Đã thông báo cho các bên liên quan |
| **Closed (hoàn thành)** | Hết thời gian theo dõi sau phát hành · Trưởng nhóm xác nhận đạt mục tiêu · Không còn việc treo liên quan |
| **Closed (không làm)** | Trưởng nhóm xác nhận · Ghi rõ lý do đóng trên thẻ · Liên kết thẻ trùng lặp/thay thế (nếu có) |

### 4.4. Quy định riêng cho một số cột

**Luồng ngược và ngoại lệ** (áp dụng cho mọi thẻ)

- Thẻ đi tuần tự từ Open đến Closed. Không kéo thẳng từ Open sang In Progress, hay từ In Progress sang Ready to Test (bỏ qua review).
- **Bị reject** ở Ready to Review hoặc Ready to Test: quay lại In Progress, giữ nguyên người phụ trách, kèm lý do và cách tái hiện lỗi.
- **Bị chặn:** sang Waiting với đủ thông tin chặn; khi gỡ chặn thì quay lại đúng cột trước đó.
- **Không làm:** từ Open hoặc Product Backlog sang Closed kèm lý do. Thẻ ở Sprint Backlog không kịp làm thì quay về Product Backlog.
- **Phát hành thất bại:** thẻ ở Ready to Release quay lại In Progress hoặc Ready to Test tùy nguyên nhân.
- **Closed không mở lại.** Cần làm tiếp thì tạo thẻ mới ở Open và liên kết thẻ cũ.
- **Hotfix khẩn cấp:** nhóm có thể rút gọn luồng, nhưng Trưởng nhóm phải đồng ý, ghi rõ trên thẻ và xem lại ở Retrospective.

**Waiting**

- Mỗi thẻ ở Waiting phải có đủ 4 thông tin: lý do, người gỡ chặn, ngày dự kiến, cột trước đó.
- Quá 2 ngày làm việc chưa gỡ được: nêu ở Daily, Điều phối viên hỗ trợ leo thang.
- Cuối sprint, thẻ vẫn ở Waiting được đưa ra Sprint Review/Retrospective để phân tích nguyên nhân.

**Today Todo**

- Chỉ chọn từ Sprint Backlog, theo thứ tự ưu tiên từ trên xuống.
- Cuối ngày dọn: thẻ chưa làm quay lại Sprint Backlog.

**In Progress**

- Mỗi thẻ chỉ có một người chịu trách nhiệm chính (có thể có người hỗ trợ).
- Thẻ đứng ở In Progress quá **3 ngày** không có tiến triển → nêu ở Daily, cân nhắc tách nhỏ hoặc nhờ giúp.

**Ready to Review / Ready to Test**

- Đây là các cột chờ, không phải cột làm việc. Thời gian chờ ở đây là lãng phí; theo dõi và giảm thiểu.
- Khi cột đạt WIP limit, mọi người ưu tiên xử lý review/test thay vì bắt đầu việc mới.

**Closed**

- Ghi rõ loại đóng: *Hoàn thành* hoặc *Không làm* (dùng nhãn).
- Lưu trữ cuối sprint.

---

## 5. WIP limit và chính sách kéo (pull)

### WIP limit

WIP (Work In Progress) limit là số thẻ tối đa được phép có trong một cột cùng lúc. Khi cột đã đầy, **không kéo thêm thẻ vào**; thay vào đó giúp làm cạn cột đó.

| Cột | Gợi ý ban đầu |
|---|---|
| Waiting | Tối đa 3 |
| Today Todo | Vừa đủ 1 ngày làm việc của người đó |
| In Progress | 1–2 thẻ mỗi người |
| Ready to Review | Tối đa 2 × số người review |
| Ready to Test | Tối đa 3–5 |
| Ready to Release | Tối đa 1 chu kỳ phát hành |

### Chính sách kéo

1. **Dừng bắt đầu, tập trung hoàn thành** (Stop starting, start finishing).
2. Thứ tự ưu tiên khi bạn rảnh tay:
   1. Gỡ chặn cho thẻ ở Waiting (của mình hoặc đồng đội).
   2. Review thẻ ở Ready to Review.
   3. Kiểm thử thẻ ở Ready to Test.
   4. Hỗ trợ đồng đội đang làm thẻ ở In Progress (pair, mob).
   5. Chỉ sau cùng mới kéo thẻ mới từ Today Todo / Sprint Backlog.
3. Khi vượt WIP limit, cả nhóm cùng nhận trách nhiệm đưa về mức cho phép, không ai bị đổ lỗi riêng.
4. Điều chỉnh WIP limit ở Retrospective dựa trên dữ liệu thực tế, không thay đổi tùy tiện giữa sprint.

---

## 6. Nhịp Scrum trên board

| Sự kiện | Thời lượng gợi ý | Tác động lên board |
|---|---|---|
| **Backlog Refinement** | 1–2 giờ/tuần | Phân loại thẻ ở Open; làm rõ, tách nhỏ, ước lượng thẻ ở Product Backlog; đưa thẻ đầu backlog đạt DoR |
| **Sprint Planning** | ≤ 2 giờ/tuần của sprint | Thống nhất Sprint Goal; kéo thẻ đạt DoR từ Product Backlog sang Sprint Backlog theo năng lực nhóm |
| **Daily Scrum** | ≤ 15 phút | Duyệt board từ phải sang trái (từ Ready to Release về In Progress): thẻ nào cần đẩy ra; chọn thẻ vào Today Todo; nêu thẻ Waiting quá hạn |
| **Sprint Review** | ≤ 1 giờ/tuần của sprint | Demo các thẻ đã Ready to Release / Released; Tester xác nhận thẻ đạt, Trưởng nhóm chuyển Closed; thẻ chưa xong quay về Product Backlog để Trưởng nhóm xếp lại |
| **Sprint Retrospective** | ≤ 45 phút/tuần của sprint | Xem lại luồng: điểm nghẽn, thẻ Waiting, tỷ lệ reject; điều chỉnh WIP limit, DoR, DoD |

Cả nhóm (Dev và Tester) tham gia mọi sự kiện. Điều phối viên chủ trì và giữ đúng khung thời gian; khi nhóm không đồng thuận về ưu tiên thì Trưởng nhóm quyết định.

**Cách đọc board trong Daily:** đi từ phải sang trái. Hỏi "Cái gì có thể đưa ra khỏi cột này hôm nay?" thay vì "Hôm qua bạn làm gì?". Cách này tập trung vào việc hoàn thành, không phải việc bận rộn.

**Cuối sprint:**

- Thẻ chưa hoàn thành (chưa tới Ready to Release) quay về Product Backlog, Trưởng nhóm xếp lại ưu tiên. Không tự động chuyển sang sprint sau.
- Thẻ Released đã được xác nhận thì chuyển Closed.
- Archive thẻ Closed.

---

## 7. Nguyên tắc làm việc hiệu quả

### Về Scrum

1. **Sprint Goal là kim chỉ nam.** Mọi thẻ trong sprint phục vụ một mục tiêu chung; khi phải đánh đổi, chọn thứ phục vụ Sprint Goal.
2. **Không thêm việc giữa sprint.** Việc mới đi vào Open; Trưởng nhóm quyết định thay thế nếu thật sự khẩn cấp.
3. **Nhóm tự tổ chức.** Nhóm tự chọn ai làm gì; không ai giao việc từ trên xuống.
4. **Trưởng nhóm quyết định ưu tiên nhanh.** Câu hỏi về yêu cầu được trả lời trong ngày để tránh dồn về Waiting.
5. **Điều phối viên gỡ vướng.** Tập trung vào thẻ Waiting và quy trình, không quản lý từng người.
6. **Retrospective luôn có hành động.** Mỗi buổi chọn 1–2 cải tiến cụ thể, có người chịu trách nhiệm, kiểm tra lại ở buổi sau.

### Về Kanban

7. **Trực quan hóa toàn bộ công việc.** Nếu việc không có trên board thì nó không tồn tại; kể cả việc "chen ngang", việc kỹ thuật, họp, hỗ trợ.
8. **Giới hạn WIP.** Làm ít việc cùng lúc, hoàn thành nhanh hơn.
9. **Quản lý luồng, không quản lý người.** Câu hỏi là "thẻ này đang bị kẹt ở đâu?" chứ không phải "người này có bận không?".
10. **Chính sách rõ ràng.** DoR, DoD, quy định chuyển cột nằm ở nơi ai cũng thấy (ví dụ ghim ở đầu board).
11. **Cải tiến từng bước** dựa trên dữ liệu (cycle time, thời gian nằm ở mỗi cột).

### Về làm việc hằng ngày

12. **Thẻ nhỏ.** Một thẻ nên hoàn thành trong 1–3 ngày. Thẻ to thì tách; thẻ nào chưa đủ rõ để tách thì làm một Spike (khảo sát có giới hạn thời gian) trước.
13. **Hoàn thành trước khi bắt đầu.** Ưu tiên đưa thẻ đang làm sang cột sau trước khi kéo thẻ mới.
14. **Review và test là ưu tiên cao.** Phản hồi review trong 1 ngày; không để đồng đội chờ.
15. **Tích hợp và deploy thường xuyên.** Merge nhỏ, CI xanh, giảm rủi ro dồn cục ở Ready to Release.
16. **Minh bạch về trạng thái thật.** Cập nhật board ngay; báo sớm khi có rủi ro. "Hầu như xong" vẫn là chưa xong.
17. **Ghi lại quyết định trên thẻ.** Lý do đổi hướng, reject, hủy, để người sau (hoặc chính bạn sau 3 tháng) hiểu.
18. **Dọn board định kỳ.** Open dọn hằng tuần; Product Backlog rà soát mỗi sprint; Closed archive cuối sprint.
19. **Tôn trọng cột Waiting.** Chặn thì ghi rõ, và chủ động gỡ; không dùng Waiting để giấu việc không muốn làm.
20. **Bảo vệ thời gian tập trung.** Hạn chế chuyển ngữ cảnh, gom họp, đặt khung giờ cho review.

---

## 8. Chỉ số gợi ý

| Chỉ số | Định nghĩa | Dùng để |
|---|---|---|
| **Lead time** | Từ lúc thẻ vào Open đến khi Released | Biết người dùng chờ bao lâu từ yêu cầu đến giá trị |
| **Cycle time** | Từ lúc vào In Progress đến Released | Đo tốc độ thực thi của nhóm |
| **Thời gian ở từng cột** | Tổng thời gian thẻ nằm ở mỗi cột | Tìm điểm nghẽn (thường ở Ready to Review/Test, Waiting) |
| **Throughput** | Số thẻ Released mỗi tuần/sprint | Dự báo năng lực |
| **Velocity** | Tổng điểm của thẻ hoàn thành mỗi sprint | Hỗ trợ Sprint Planning |
| **Tỷ lệ reject** | % thẻ bị đẩy ngược từ Review/Test về In Progress | Đánh giá chất lượng đầu vào cổng và DoD |
| **Số thẻ Waiting và thời gian chờ** | Số thẻ và số ngày ở Waiting | Đo mức độ phụ thuộc bên ngoài |
| **Burndown / CFD** | Biểu đồ công việc còn lại / biểu đồ luồng tích lũy | Trực quan hóa tiến độ sprint và điểm nghẽn |

> Dùng chỉ số để hiểu và cải tiến hệ thống, không để so sánh hay đánh giá cá nhân.

---

## 9. Lỗi thường gặp (anti-patterns)

| Dấu hiệu | Vấn đề | Cách xử lý |
|---|---|---|
| Open có hàng trăm thẻ | Trở thành bãi rác, mất niềm tin vào board | Trưởng nhóm phân loại hằng tuần; đóng thẻ cũ không còn giá trị |
| Thẻ nằm ở Waiting hàng tuần | Che giấu việc bị chặn, không ai chịu trách nhiệm | Ghi rõ người gỡ chặn và ngày dự kiến; leo thang ở Daily |
| In Progress có quá nhiều thẻ | Chuyển ngữ cảnh, không thẻ nào xong | Giữ WIP limit; hỗ trợ đồng đội hoàn thành |
| Ready to Review/Test chất đống | Điểm nghẽn ở khâu chờ | Đặt khung giờ review; ưu tiên review trước khi làm mới |
| Kéo thẻ qua cột khi chưa đạt DoD | Chất lượng giảm, nợ kỹ thuật tăng | Người kéo phải tự kiểm tra checklist; nêu ở Retrospective |
| Today Todo dài như backlog | Không thực tế, cảm giác thất bại mỗi ngày | Chỉ chọn vừa đủ 1 ngày |
| Thêm việc thẳng vào sprint | Phá cam kết, mất Sprint Goal | Đi qua Open và Trưởng nhóm; đánh đổi bằng việc tương đương |
| Ready to Release tồn đọng | Giá trị không đến người dùng | Rút ngắn chu kỳ phát hành; tự động hóa deploy |
| Không bao giờ đóng thẻ Released | Board rối, không đo được kết quả | Xác nhận với Trưởng nhóm sau thời gian theo dõi |
| Sprint Goal chỉ là danh sách thẻ | Mất định hướng | Viết Sprint Goal là một câu về giá trị/kết quả |
| Retrospective không có hành động | Không cải tiến | Mỗi buổi chọn 1–2 hành động, kiểm tra lại ở buổi sau |

---

## 10. Checklist nhanh

### Đầu sprint (Sprint Planning)

- [ ] Sprint Goal được viết thành một câu rõ ràng
- [ ] Mọi thẻ trong Sprint Backlog đạt DoR
- [ ] Tổng ước lượng phù hợp với velocity/năng lực thực tế
- [ ] Đã xử lý hoặc có kế hoạch cho các thẻ còn ở Waiting từ sprint trước
- [ ] Đã xem lại WIP limit và các chính sách (DoR, DoD)

### Hằng ngày (Daily Scrum)

- [ ] Duyệt board từ phải sang trái
- [ ] Thẻ ở Ready to Review/Test có người nhận chưa?
- [ ] Thẻ ở Waiting quá 2 ngày đã được leo thang chưa?
- [ ] Đã chọn Today Todo vừa đủ cho hôm nay
- [ ] Không cột nào vượt WIP limit
- [ ] Board phản ánh đúng thực tế

### Khi chuyển thẻ

- [ ] Đã kiểm tra điều kiện vào cột (DoR/DoD tương ứng)
- [ ] Đã cập nhật người phụ trách và link liên quan
- [ ] Nếu chuyển ngược/vào Waiting/Closed: đã ghi lý do trên thẻ

### Cuối sprint (Review và Retrospective)

- [ ] Demo các thẻ đã xong; Tester và Trưởng nhóm xác nhận
- [ ] Thẻ chưa xong quay lại Product Backlog, Trưởng nhóm xếp lại ưu tiên
- [ ] Thẻ Released đã xác nhận được chuyển Closed và archive
- [ ] Xem lại chỉ số: cycle time, thời gian ở từng cột, tỷ lệ reject
- [ ] Chọn 1–2 hành động cải tiến với người chịu trách nhiệm
- [ ] Điều chỉnh WIP limit, DoR, DoD nếu cần
