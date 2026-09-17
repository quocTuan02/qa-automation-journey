# Bài 04: List, Tuple, Dict, Set nâng cao + xử lý String

**Tháng 1 – Tuần 2** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Thao tác thành thạo với các cấu trúc dữ liệu — đây là kiểu dữ liệu bạn sẽ dùng liên tục để lưu test data, danh sách locator, kết quả test.

## 📘 Nội dung học
1. **List**: indexing, slicing, `append/remove/insert/pop`, **list comprehension** (`[x for x in list if ...]`).
2. **Tuple**: bất biến (immutable), khi nào dùng tuple thay vì list.
3. **Dict**: key-value, `.get()`, `.keys()/.values()/.items()`, duyệt dict bằng `for k, v in dict.items()`.
4. **Set**: phần tử không trùng lặp, các phép toán tập hợp (union, intersection) — hữu ích khi so sánh 2 tập dữ liệu test.
5. **Xử lý string**: `split()`, `join()`, `strip()`, `replace()`, `.format()`/f-string, kiểm tra `in`.

## 📚 Tài liệu tham khảo
- [W3Schools – Python Lists](https://www.w3schools.com/python/python_lists.asp), [Dictionaries](https://www.w3schools.com/python/python_dictionaries.asp), [Sets](https://www.w3schools.com/python/python_sets.asp)
- [Real Python – List Comprehensions](https://realpython.com/list-comprehension-python/)
- [Python.org – Data Structures](https://docs.python.org/3/tutorial/datastructures.html)

## ✍️ Bài tập
1. Cho danh sách số `[3, 7, 2, 9, 4, 1, 8]`: dùng list comprehension lọc ra các số chẵn, và các số > 5.
2. Viết chương trình đếm số lần xuất hiện của mỗi ký tự trong 1 chuỗi, lưu kết quả vào 1 `dict`.
3. Cho 2 danh sách sản phẩm (list các dict, mỗi dict có `name`, `price`), viết hàm gộp 2 danh sách và loại bỏ sản phẩm trùng tên (dùng `set` hoặc dict theo key).
4. Viết chương trình nhận vào 1 câu, in ra từng từ theo thứ tự ngược lại (dùng `split()` + `join()`).
5. Mô phỏng test data: viết 1 `dict` chứa danh sách tài khoản test `{"username": ..., "password": ..., "role": ...}` cho 5 user, viết hàm lọc ra danh sách user có `role == "admin"`.
