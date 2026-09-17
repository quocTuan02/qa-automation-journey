# Bài 10: Subquery, hàm Aggregate, CASE WHEN

**Tháng 1 – Tuần 4** | Thời lượng gợi ý: 3 ngày + 1 ngày ôn tập tổng kết tháng 1

## 🎯 Mục tiêu
- Hoàn thiện bộ kỹ năng SQL đủ dùng trong công việc test: truy vấn lồng nhau, tính toán tổng hợp, tạo cột điều kiện.

## 📘 Nội dung học

1. **Subquery (truy vấn con)**: là 1 câu `SELECT` nằm lồng bên trong 1 câu truy vấn khác — dùng khi kết quả cần so sánh không phải là 1 giá trị cố định mà phải tính toán trước bằng 1 truy vấn riêng. Subquery có thể đặt trong `WHERE` (lọc theo 1 giá trị tính toán được), trong `FROM` (coi kết quả subquery như 1 bảng tạm), hoặc trong `SELECT` (tính thêm 1 cột).

   ```sql
   -- Subquery trong WHERE: tim track co gia cao hon gia trung binh cua TAT CA track
   SELECT Name, UnitPrice
   FROM tracks
   WHERE UnitPrice > (SELECT AVG(UnitPrice) FROM tracks);

   -- Subquery trong FROM: coi ket qua tinh tong hoa don theo khach hang nhu 1 "bang tam"
   SELECT tam.CustomerId, tam.tong_tien
   FROM (
       SELECT CustomerId, SUM(Total) AS tong_tien
       FROM invoices
       GROUP BY CustomerId
   ) AS tam
   WHERE tam.tong_tien > 45;
   ```

2. **Hàm Aggregate**: các hàm tính toán trên **nhiều dòng** rồi trả về **1 giá trị duy nhất** — `COUNT` đếm số dòng, `SUM` tính tổng, `AVG` tính trung bình, `MIN`/`MAX` tìm giá trị nhỏ nhất/lớn nhất.

   ```sql
   SELECT
       COUNT(*) AS tong_so_track,
       AVG(UnitPrice) AS gia_trung_binh,
       MIN(UnitPrice) AS gia_thap_nhat,
       MAX(UnitPrice) AS gia_cao_nhat
   FROM tracks;
   ```

3. **`CASE WHEN`**: tạo ra 1 cột mới trong kết quả truy vấn, giá trị của cột đó phụ thuộc vào điều kiện — giống như viết `if/elif/else` (Bài 02) nhưng ngay trong câu SQL, để phân loại dữ liệu ngay khi truy vấn thay vì phải xử lý lại bằng code sau đó.

   ```sql
   SELECT
       c.FirstName,
       SUM(i.Total) AS tong_chi_tieu,
       CASE
           WHEN SUM(i.Total) > 45 THEN 'VIP'
           WHEN SUM(i.Total) BETWEEN 20 AND 45 THEN 'Thuong'
           ELSE 'Moi'
       END AS phan_loai
   FROM customers c
   INNER JOIN invoices i ON c.CustomerId = i.CustomerId
   GROUP BY c.FirstName;
   ```

4. **`UNION` / `UNION ALL`**: gộp kết quả của 2 (hay nhiều) câu `SELECT` có cùng số cột và kiểu dữ liệu tương ứng thành 1 bảng kết quả duy nhất. `UNION` tự loại bỏ dòng trùng lặp, `UNION ALL` giữ nguyên tất cả (nhanh hơn vì không cần so sánh trùng lặp).

   ```sql
   -- Gop danh sach ten tu 2 bang khac nhau (vi du minh hoa cu phap)
   SELECT FirstName AS ten FROM customers
   UNION
   SELECT FirstName AS ten FROM employees;
   ```

5. **Thực hành viết truy vấn để verify dữ liệu test**: đây là ứng dụng thực tế nhất trong công việc — sau khi test 1 chức năng qua UI/API, tester dùng SQL để xác minh trực tiếp trong database rằng dữ liệu được lưu đúng như kỳ vọng, không chỉ tin vào những gì hiển thị trên màn hình.

   ```sql
   -- Kich ban: vua "tao don hang" qua UI cho khach hang CustomerId = 7
   -- -> kiem tra du lieu trong bang invoices va invoice_items co khop khong

   -- 1. Kiem tra hoa don moi nhat cua khach hang co duoc tao dung khong
   SELECT * FROM invoices WHERE CustomerId = 7 ORDER BY InvoiceDate DESC LIMIT 1;

   -- 2. Kiem tra tong tien tren hoa don co khop voi tong cac dong san pham khong
   SELECT ii.InvoiceId, SUM(ii.UnitPrice * ii.Quantity) AS tong_tinh_tay, i.Total AS tong_luu_trong_db
   FROM invoice_items ii
   JOIN invoices i ON ii.InvoiceId = i.InvoiceId
   WHERE i.InvoiceId = 999   -- thay bang InvoiceId thuc te vua tao
   GROUP BY ii.InvoiceId, i.Total;
   ```

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
