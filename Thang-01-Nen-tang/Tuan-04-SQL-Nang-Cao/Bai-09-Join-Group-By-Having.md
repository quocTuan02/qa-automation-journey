# Bài 09: SQL nâng cao cho tester — JOIN, GROUP BY, HAVING

**Tháng 1 – Tuần 4** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Nâng cấp SQL từ mức cơ bản (SELECT/WHERE bạn đã biết) lên mức đủ dùng để **chuẩn bị và kiểm tra test data** — đúng yêu cầu JD.

## 📘 Nội dung học
1. **Ôn nhanh**: `SELECT`, `WHERE`, `ORDER BY`, `LIKE`, `DISTINCT`.
2. **JOIN**: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN` — khi nào dùng loại nào, vẽ sơ đồ Venn để dễ nhớ.
3. **GROUP BY**: gom nhóm dữ liệu, kết hợp hàm tổng hợp.
4. **HAVING**: lọc sau khi đã `GROUP BY` (khác `WHERE` lọc trước khi gom nhóm).
5. Liên hệ QA thực tế: dùng JOIN + GROUP BY để kiểm tra dữ liệu liên bảng đúng như nghiệp vụ mô tả (vd: đếm số đơn hàng theo từng khách hàng để verify tính năng báo cáo).

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
