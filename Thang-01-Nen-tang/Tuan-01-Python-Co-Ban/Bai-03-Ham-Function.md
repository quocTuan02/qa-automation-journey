# Bài 03: Hàm (function), tham số, return, scope biến

**Tháng 1 – Tuần 1** | Thời lượng gợi ý: 2 ngày + 1 ngày ôn tập tuần

## 🎯 Mục tiêu
- Viết được hàm để tái sử dụng code — kỹ năng bắt buộc vì mọi automation script đều được tổ chức thành hàm/method.

## 📘 Nội dung học

1. **Định nghĩa hàm**: `def ten_ham(tham_so):` gói 1 đoạn code lại thành 1 khối có tên, để gọi lại nhiều lần thay vì copy-paste. Đây là bước đầu tiên hướng tới việc viết "test function" sau này (mỗi test trong Pytest cũng chỉ là 1 hàm `def test_...():`).

   ```python
   def kiem_tra_so_nguyen_to(n):
       if n < 2:
           return False
       for i in range(2, n):
           if n % i == 0:
               return False
       return True

   print(kiem_tra_so_nguyen_to(7))   # True
   print(kiem_tra_so_nguyen_to(8))   # False
   ```

2. **Tham số**: tham số thường (bắt buộc truyền vào theo đúng thứ tự), tham số mặc định (default — có sẵn giá trị nếu người gọi không truyền), `*args`/`**kwargs` (nhận số lượng tham số không cố định, biết sơ qua để không bỡ ngỡ khi đọc code thư viện).

   ```python
   def dang_nhap(username, password, remember_me=False):
       print(f"Dang nhap: {username}/{password}, remember_me={remember_me}")

   dang_nhap("standard_user", "secret_sauce")               # remember_me dung gia tri mac dinh False
   dang_nhap("standard_user", "secret_sauce", remember_me=True)
   ```

3. **`return`**: hàm dùng `return` sẽ trả kết quả về cho nơi gọi nó để dùng tiếp; hàm không có `return` (hoặc `return` không kèm giá trị) sẽ trả về `None`. Phân biệt rõ 2 loại này quan trọng vì hàm kiểm tra điều kiện (assert) luôn cần `return` giá trị `True`/`False`.

   ```python
   def cong(a, b):
       return a + b

   ket_qua = cong(2, 3)
   print(ket_qua)          # 5, dùng lại được vì hàm có return

   def in_loi(msg):
       print(f"LOI: {msg}")   # không có return -> gọi hàm này chỉ để in, không lấy giá trị

   x = in_loi("test fail")
   print(x)                 # None
   ```

4. **Phạm vi biến (scope)**: biến khai báo bên trong hàm (local) chỉ tồn tại và dùng được bên trong hàm đó; biến khai báo bên ngoài (global) dùng được ở mọi nơi. Hiểu rõ scope giúp tránh lỗi "biến không tồn tại" khi code lớn dần.

   ```python
   bien_toan_cuc = "base_url mac dinh"

   def hien_thi_url():
       bien_cuc_bo = "chi ton tai trong ham nay"
       print(bien_toan_cuc)     # doc duoc bien global, khong loi
       print(bien_cuc_bo)

   hien_thi_url()
   # print(bien_cuc_bo)   # neu bo comment dong nay -> loi NameError vi bien_cuc_bo da het pham vi
   ```

5. **Docstring**: đoạn mô tả ngắn đặt ngay dòng đầu tiên trong hàm bằng `"""..."""`, giải thích hàm dùng để làm gì — thói quen bắt buộc khi viết automation framework để đồng nghiệp (và cả IDE) hiểu ngay mục đích hàm mà không cần đọc hết code bên trong.

   ```python
   def is_valid_email(email):
       """Kiem tra chuoi email co dung dinh dang co ban (co @ va dau cham) hay khong."""
       return "@" in email and "." in email

   print(is_valid_email("tester@example.com"))   # True
   ```

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
