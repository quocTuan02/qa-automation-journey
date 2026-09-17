# Bài 01: Cài đặt môi trường + Biến, kiểu dữ liệu, toán tử

**Tháng 1 – Tuần 1** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Cài xong môi trường code trên máy để dùng suốt lộ trình.
- Đọc/viết được các lệnh Python cơ bản nhất: biến, kiểu dữ liệu, toán tử, input/output.

## 📘 Nội dung học

1. **Cài đặt môi trường**
   - Cài Python 3.x (kiểm tra bằng `python --version`).
   - Cài VSCode + extension "Python" (Microsoft) và "Pylance".
   - Chạy thử file `.py` đầu tiên: `print("Hello QA")`.

   > Đây là bước "bắt tay" đầu tiên với máy tính bằng code thay vì click chuột — mọi công cụ automation sau này (Playwright, Pytest...) đều chạy trên nền Python vừa cài.

2. **Biến (variable)**: là một "cái hộp có tên" để lưu tạm 1 giá trị trong lúc chương trình chạy, để dùng lại nhiều lần mà không cần gõ lại giá trị đó. Quy tắc đặt tên: chỉ gồm chữ/số/gạch dưới, không bắt đầu bằng số, nên đặt tên có nghĩa (vd `username` chứ không đặt `x`).

   ```python
   # Demo: biến lưu dữ liệu test — thay vì gõ lại chuỗi này nhiều lần,
   # ta lưu vào biến và tái sử dụng khi viết test sau này
   ten_test_case = "Kiem tra dang nhap thanh cong"
   username = "standard_user"
   password = "secret_sauce"
   print(ten_test_case, "-", username)
   ```

3. **Kiểu dữ liệu cơ bản**: `int` (số nguyên), `float` (số thập phân), `str` (chuỗi văn bản), `bool` (đúng/sai `True`/`False`). Python tự nhận diện kiểu dữ liệu khi bạn gán giá trị — dùng hàm `type()` để kiểm tra lại xem biến đang là kiểu gì.

   ```python
   so_luong_test_case = 24        # int
   ty_le_pass = 95.5               # float
   ten_du_an = "QA Automation"     # str
   da_pass = True                  # bool

   print(type(so_luong_test_case))  # <class 'int'>
   print(type(ty_le_pass))          # <class 'float'>
   ```

4. **Toán tử**: số học (`+ - * / // % **`), so sánh (`== != > < >= <=`), logic (`and or not`). Toán tử so sánh cực quan trọng vì đây chính là "não bộ" của mọi câu lệnh `assert` khi viết test sau này (so sánh kết quả thực tế với kết quả mong đợi).

   ```python
   # Demo: toán tử so sánh — chính là cách 1 test "assert" hoạt động
   ket_qua_mong_doi = 200
   ket_qua_thuc_te = 200
   print(ket_qua_thuc_te == ket_qua_mong_doi)   # True -> test PASS
   print(10 % 3)                                 # 1 (số dư, hay dùng để kiểm tra số chẵn/lẻ)
   ```

5. **Input/Output**: `print()` để in dữ liệu ra màn hình (dùng f-string `f"..."` để chèn biến vào chuỗi cho dễ đọc), `input()` để nhận dữ liệu người dùng gõ vào (luôn trả về kiểu `str`, cần ép kiểu nếu muốn tính toán số).

   ```python
   ten = input("Nhap ten tester: ")
   tuoi = int(input("Nhap tuoi: "))   # ep kieu ve int de tinh toan duoc
   print(f"Xin chao {ten}, ban {tuoi} tuoi.")
   ```

6. **Comment**: dòng ghi chú bắt đầu bằng `#`, Python bỏ qua không chạy — dùng để giải thích lý do đoạn code viết như vậy cho người đọc sau (kể cả chính mình sau này).

   ```python
   # Test data cho case login hop le (khong phai code chay, chi la ghi chu)
   username = "standard_user"
   ```

## 📚 Tài liệu tham khảo
- [Python.org – The Python Tutorial (chương 3)](https://docs.python.org/3/tutorial/introduction.html) — tài liệu chính thức.
- [W3Schools Python Variables](https://www.w3schools.com/python/python_variables.asp) — ví dụ ngắn gọn, dễ tra cứu.
- [Real Python – Basic Data Types](https://realpython.com/python-data-types/) — giải thích sâu hơn, có ví dụ thực tế.
- Kênh YouTube tiếng Việt: "Khoa Pham" hoặc "CodeGym Vietnam" — tìm playlist "Học Python cơ bản".

## ✍️ Bài tập
1. Cài đặt xong môi trường, chụp lại màn hình chạy được `print("Hello QA")`.
2. Viết chương trình nhận vào tên và tuổi (dùng `input()`), in ra câu: `"Xin chào <tên>, bạn <tuổi> tuổi."`
3. Viết chương trình tính diện tích và chu vi hình chữ nhật khi biết chiều dài, chiều rộng (nhập từ bàn phím).
4. Viết chương trình đổi độ C sang độ F: `F = C * 9/5 + 32`.
5. (Nâng cao) Viết chương trình nhận 2 số, in ra kết quả của cả 4 phép toán `+ - * /` cùng lúc.
