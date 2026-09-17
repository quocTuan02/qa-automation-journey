# Bài 10: Subquery, hàm Aggregate, CASE WHEN

**Tháng 1 – Tuần 4** | Thời lượng gợi ý: 3 ngày + 1 ngày ôn tập tổng kết tháng 1

## 🎯 Mục tiêu
- Hoàn thiện bộ kỹ năng SQL đủ dùng trong công việc test: truy vấn lồng nhau, tính toán tổng hợp, tạo cột điều kiện.

## 📘 Nội dung học
1. **Subquery (truy vấn con)**: subquery trong `WHERE`, trong `FROM`, trong `SELECT`.
2. **Hàm Aggregate**: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.
3. **`CASE WHEN`**: tạo cột phân loại/điều kiện trong kết quả truy vấn (vd gắn nhãn "VIP"/"Thường" theo tổng chi tiêu).
4. **`UNION` / `UNION ALL`** (biết sơ qua): gộp kết quả nhiều truy vấn.
5. Thực hành viết truy vấn để **verify dữ liệu test** — mô phỏng đúng công việc: "kiểm tra sau khi tạo đơn hàng, dữ liệu trong bảng `orders` và `order_items` có khớp không".

## 📚 Tài liệu tham khảo
- [W3Schools – SQL Subqueries](https://www.w3schools.com/sql/sql_subqueries.asp), [CASE](https://www.w3schools.com/sql/sql_case.asp)
- [Mode Analytics – SQL Tutorial (Subqueries)](https://mode.com/sql-tutorial/sql-sub-queries/)
- [SQLZoo](https://sqlzoo.net/) — luyện tập SQL online có chấm điểm ngay, rất hợp để luyện phản xạ viết query.

## ✍️ Bài tập
1. Tìm track có giá (`unit_price`) cao hơn giá trung bình của tất cả track (dùng subquery trong `WHERE`).
2. Với mỗi khách hàng, phân loại `CASE WHEN` tổng chi tiêu: `> 45` là "VIP", `20-45` là "Thường", còn lại là "Mới" — xuất kèm tên khách hàng.
3. Viết query đếm số lượng nhân viên (`employees`) quản lý theo từng "manager" (dùng self-join hoặc subquery).
4. Viết 1 kịch bản kiểm thử bằng lời: giả sử vừa test tính năng "tạo đơn hàng", liệt kê 3 câu SQL bạn sẽ chạy để xác minh dữ liệu được lưu đúng (checklist việc dùng SQL trong test thực tế).
5. **Ôn tập tổng kết tháng 1**: viết lại 1 file tổng hợp `on_tap_thang1.md` liệt kê những gì đã học (Python cơ bản, OOP, Git, SQL) và tự đánh giá phần nào còn yếu cần ôn thêm trước khi qua tháng 2 (Automation).
