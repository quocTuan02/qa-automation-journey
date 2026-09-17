# Bài 03: Hàm (function), tham số, return, scope biến

**Tháng 1 – Tuần 1** | Thời lượng gợi ý: 2 ngày + 1 ngày ôn tập tuần

## 🎯 Mục tiêu
- Viết được hàm để tái sử dụng code — kỹ năng bắt buộc vì mọi automation script đều được tổ chức thành hàm/method.

## 📘 Nội dung học
1. **Định nghĩa hàm**: `def ten_ham(tham_so):`, gọi hàm.
2. **Tham số**: tham số thường, tham số mặc định (default), `*args`, `**kwargs` (biết sơ qua).
3. **`return`**: hàm trả về giá trị vs hàm không trả về (`None`).
4. **Phạm vi biến (scope)**: biến local vs global.
5. **Docstring**: viết mô tả ngắn cho hàm (thói quen tốt, dùng nhiều khi viết test).

## 📚 Tài liệu tham khảo
- [Python.org – Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
- [W3Schools – Python Functions](https://www.w3schools.com/python/python_functions.asp)
- [Real Python – Defining Your Own Python Function](https://realpython.com/defining-your-own-python-function/)

## ✍️ Bài tập
1. Viết hàm `is_prime(n)` trả về `True/False` số nguyên tố (tái sử dụng từ bài 2, giờ đóng gói thành hàm).
2. Viết hàm `factorial(n)` tính giai thừa.
3. Viết hàm `max_min(list_so)` trả về tuple `(số lớn nhất, số nhỏ nhất)` của 1 danh sách — **không dùng `max()`/`min()` có sẵn**.
4. Viết hàm `sort_list(list_so)` sắp xếp danh sách tăng dần — không dùng `sorted()`/`.sort()` có sẵn (gợi ý: thuật toán bubble sort).
5. **Ôn tập tuần 1**: gộp tất cả bài tập tuần này thành 1 file `on_tap_tuan1.py`, chạy thử toàn bộ, đẩy lên GitHub (nếu đã có tài khoản) hoặc lưu lại để tuần 3 push lên.
