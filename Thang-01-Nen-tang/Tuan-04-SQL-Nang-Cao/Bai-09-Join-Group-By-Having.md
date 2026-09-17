# Bài 09: SQL nâng cao cho tester — JOIN, GROUP BY, HAVING

**Tháng 1 – Tuần 4** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Nâng cấp SQL từ mức cơ bản (SELECT/WHERE bạn đã biết) lên mức đủ dùng để **chuẩn bị và kiểm tra test data** — đúng yêu cầu JD.

## 📘 Nội dung học

1. **Ôn nhanh**: `SELECT cot FROM bang WHERE dieu_kien ORDER BY cot [ASC|DESC]` là cấu trúc câu truy vấn cơ bản bạn đã quen; `LIKE` dùng để tìm chuỗi gần đúng (`%` là ký tự đại diện cho bất kỳ đoạn nào), `DISTINCT` loại bỏ dòng kết quả trùng lặp.

   ```sql
   SELECT FirstName, LastName, Email
   FROM customers
   WHERE Country = 'USA' AND Email LIKE '%gmail.com'
   ORDER BY LastName ASC;

   SELECT DISTINCT Country FROM customers;   -- liet ke cac quoc gia, khong lap lai
   ```

2. **JOIN**: dùng để kết hợp dữ liệu từ 2 bảng có liên quan qua 1 cột chung (thường là khóa chính/khóa ngoại). `INNER JOIN` chỉ lấy các dòng khớp ở **cả 2** bảng; `LEFT JOIN` lấy **toàn bộ** dòng của bảng bên trái, dòng nào không khớp bên phải sẽ để `NULL`; `RIGHT JOIN` làm ngược lại.

   ```sql
   -- INNER JOIN: chi lay khach hang CO hoa don
   SELECT c.FirstName, c.LastName, i.InvoiceId, i.Total
   FROM customers c
   INNER JOIN invoices i ON c.CustomerId = i.CustomerId;

   -- LEFT JOIN: lay TAT CA khach hang, ke ca chua tung co hoa don nao (i.InvoiceId se la NULL)
   SELECT c.FirstName, c.LastName, i.InvoiceId
   FROM customers c
   LEFT JOIN invoices i ON c.CustomerId = i.CustomerId;
   ```

3. **GROUP BY**: gom các dòng có cùng giá trị ở 1 cột thành 1 nhóm, thường đi kèm hàm tổng hợp (`COUNT`, `SUM`...) để tính toán theo từng nhóm thay vì theo từng dòng riêng lẻ.

   ```sql
   -- Dem so hoa don theo tung khach hang
   SELECT c.CustomerId, c.FirstName, COUNT(i.InvoiceId) AS so_hoa_don
   FROM customers c
   INNER JOIN invoices i ON c.CustomerId = i.CustomerId
   GROUP BY c.CustomerId, c.FirstName;
   ```

4. **HAVING**: giống `WHERE` nhưng lọc **sau khi** đã `GROUP BY` — vì `WHERE` chạy trước khi gom nhóm nên không thể lọc theo kết quả của hàm tổng hợp (`COUNT`, `SUM`...), phải dùng `HAVING` cho việc này.

   ```sql
   -- Tim khach hang co tong chi tieu (SUM) lon hon 40
   SELECT c.CustomerId, c.FirstName, SUM(i.Total) AS tong_chi_tieu
   FROM customers c
   INNER JOIN invoices i ON c.CustomerId = i.CustomerId
   GROUP BY c.CustomerId, c.FirstName
   HAVING SUM(i.Total) > 40;
   ```

5. **Liên hệ QA thực tế**: khi test 1 tính năng "báo cáo doanh số theo khách hàng", tester không chỉ kiểm tra UI hiển thị đúng mà còn cần tự viết query xác minh **số liệu gốc trong database** khớp với số liệu hiển thị trên màn hình — đây chính là lúc JOIN + GROUP BY + HAVING phát huy tác dụng.

   ```sql
   -- Kich ban: UI bao cao hien thi "Khach hang X co 5 don hang, tong 120 USD"
   -- -> Tester chay query nay de doi chieu ngay voi du lieu that trong DB:
   SELECT c.FirstName, COUNT(i.InvoiceId) AS so_don, SUM(i.Total) AS tong_tien
   FROM customers c
   INNER JOIN invoices i ON c.CustomerId = i.CustomerId
   WHERE c.CustomerId = 7
   GROUP BY c.FirstName;
   ```

## 📚 Tài liệu tham khảo
- [W3Schools – SQL Joins](https://www.w3schools.com/sql/sql_join.asp), [GROUP BY](https://www.w3schools.com/sql/sql_groupby.asp), [HAVING](https://www.w3schools.com/sql/sql_having.asp)
- [Mode Analytics – SQL Tutorial (Joins)](https://mode.com/sql-tutorial/sql-joins/) — trực quan, có hình minh họa rất dễ hiểu.
- [SQLite](https://www.sqlite.org/index.html) hoặc [DB Browser for SQLite](https://sqlitebrowser.org/) để thực hành không cần cài server nặng.
- Database mẫu để luyện: [Chinook Database](https://github.com/lerocha/chinook-database) (dữ liệu cửa hàng nhạc, có sẵn nhiều bảng liên kết).

## ✍️ Bài tập
Tải Chinook database, dùng DB Browser for SQLite hoặc `sqlite3`, viết các query sau:
1. Liệt kê tên khách hàng (`customers`) cùng tổng số hóa đơn (`invoices`) của họ, dùng `INNER JOIN` + `GROUP BY`.
2. Tìm các khách hàng có tổng chi tiêu (`SUM(total)`) lớn hơn 40, dùng `HAVING`.
3. Liệt kê các track (`tracks`) kèm tên album và tên nghệ sĩ tương ứng (JOIN qua 3 bảng: `tracks`, `albums`, `artists`).
4. Dùng `LEFT JOIN` để tìm khách hàng **chưa từng** có hóa đơn nào (nếu Chinook không có case này, thử tự thêm 1 dòng customer mới để test).
5. Đếm số lượng track theo từng thể loại (`genres`), sắp xếp giảm dần theo số lượng.
