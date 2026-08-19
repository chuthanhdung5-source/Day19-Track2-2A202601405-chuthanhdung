# Reflection — Lab 19

**Tên:** _Chu Thành Dũng_
**Cohort:** _A20-Track2_
**Path đã chạy:** _lite_

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Dựa trên kết quả đo thực tế từ `python scripts/benchmark.py`:
- `exact` (15 queries): **Keyword (BM25)** và **Hybrid** cùng đạt Precision@10 cao nhất là **96.7%** (vượt Semantic 88.7%) do khớp chính xác các thuật ngữ gốc.
- `paraphrase` (15 queries): **Keyword (33.3%)** nhỉnh hơn Hybrid (32.0%) và Semantic (24.0%) do mô hình mặc định `bge-small-en` hạn chế với tiếng Việt diễn đạt lại.
- `mixed` (20 queries): **Hybrid thắng tuyệt đối 100.0%** (so với BM25 97.0% và Semantic 98.5%) nhờ RRF dung hòa cả từ khóa và ngữ nghĩa.
- **Khi nào không dùng Hybrid?**: Khi cần độ trễ cực thấp. BM25 có P99 chỉ **1.8ms** (nhanh hơn ~80 lần so với Hybrid P99 = **146.0ms**). Nếu truy vấn chỉ là tra cứu mã/từ khóa chính xác (`exact`), pure BM25 đạt 96.7% tương đương Hybrid nhưng tối ưu chi phí và tốc độ vượt trội.

---

## Điều ngạc nhiên nhất khi làm lab này

Mô hình embedding `bge-small-en` gặp khó khăn với tiếng Việt diễn đạt lại (`paraphrase` chỉ 24.0%), nhưng khi kết hợp qua thuật toán RRF ở loại `mixed`, Hybrid lại đạt độ chính xác hoàn hảo 100.0%.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
