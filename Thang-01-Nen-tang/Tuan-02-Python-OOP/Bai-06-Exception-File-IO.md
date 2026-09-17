# Bài 06: Exception Handling & Đọc/ghi file (CSV, JSON)

**Tháng 1 – Tuần 2** | Thời lượng gợi ý: 2 ngày + 1 ngày bài tập tổng hợp

## 🎯 Mục tiêu
- Xử lý lỗi không làm crash chương trình — automation script chạy hàng loạt test cần biết bắt lỗi để không dừng cả bộ test khi 1 case fail.
- Đọc/ghi file CSV, JSON — 2 định dạng phổ biến nhất để lưu test data.

## 📘 Nội dung học
1. **`try / except / else / finally`**: bắt lỗi cụ thể (`except ValueError:`) vs bắt lỗi chung (`except Exception as e:`).
2. **`raise`**: tự tạo và ném lỗi.
3. **Đọc/ghi file text** cơ bản: `open()`, `with open(...) as f:`.
4. **Module `csv`**: `csv.reader`, `csv.DictReader`, `csv.writer`.
5. **Module `json`**: `json.load`, `json.dump`, `json.loads`, `json.dumps` — vì response API sau này là JSON.

## 📚 Tài liệu tham khảo
- [Python.org – Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)
- [Real Python – Reading and Writing Files](https://realpython.com/read-write-files-python/)
- [Real Python – Working With JSON Data](https://realpython.com/python-json/)
- [Python.org – csv module](https://docs.python.org/3/library/csv.html)

## ✍️ Bài tập
1. Viết hàm chia 2 số có xử lý `try/except` cho lỗi chia cho 0 (`ZeroDivisionError`) và lỗi nhập sai kiểu (`ValueError`).
2. Tạo file `test_data.csv` chứa danh sách tài khoản test (`username,password,role`), viết chương trình đọc file bằng `csv.DictReader` và in ra danh sách user có `role=admin`.
3. Viết chương trình đọc 1 file JSON mô phỏng response API (vd danh sách sản phẩm), lọc ra sản phẩm có `price > 100`, ghi kết quả lọc được ra 1 file JSON mới.
4. **Bài tập tổng hợp tuần 2**: Viết class `Product` (bài 05) + đọc dữ liệu từ CSV (bài này) + xử lý lỗi khi dòng dữ liệu bị thiếu/sai định dạng (bỏ qua dòng lỗi, in cảnh báo thay vì crash). Đẩy code lên GitHub nếu tuần 3 đã có repo, hoặc lưu lại.
