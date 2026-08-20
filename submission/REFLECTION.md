# Reflection — Lab 19

**Tên:** Trương Đan Vi
**Cohort:** 4
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 queries, hybrid đạt Precision@10 trung bình cao nhất (78,6%),
nhỉnh hơn BM25 (77,8%) và vector (73,2%). Với nhóm `mixed`, hybrid thắng rõ nhất
(100%) vì RRF kết hợp được tín hiệu khớp từ khóa của BM25 với độ tương đồng ngữ
nghĩa của vector. Với `exact`, BM25 và hybrid cùng đạt 96,7%; truy vấn chứa đúng
thuật ngữ nên lexical matching đã đủ tốt. Ở nhóm `paraphrase`, kết quả lần chạy
này khá bất ngờ: BM25 đạt 33,3%, hybrid 32,0% và vector chỉ 24,0%. Điều đó cho
thấy embedding hiện tại chưa biểu diễn tốt mọi diễn đạt tiếng Việt trong golden
set, nên không thể mặc định vector luôn thắng paraphrase.

Tôi sẽ không dùng hybrid khi truy vấn cần khớp chính xác mã, tên riêng hoặc thuật
ngữ cố định—BM25 nhanh hơn và dễ giải thích. Tôi chọn pure vector khi người dùng
diễn đạt tự nhiên, từ vựng khác tài liệu và benchmark theo miền đã chứng minh
semantic retrieval tốt hơn. Hybrid phù hợp khi query có cả từ khóa chính xác lẫn
ý nghĩa diễn đạt, nhưng phải chấp nhận thêm độ trễ và độ phức tạp vận hành.

---

## Điều ngạc nhiên nhất khi làm lab này

Warmup loại bỏ cold start nhưng không đảm bảo latency giảm: inference CPU kéo dài
có thể làm máy nóng và tăng tail latency; vì vậy cần đọc cả P50, P95 và P99 thay
vì chỉ nhìn một request.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: không
