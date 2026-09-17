# Bài 02: Cấu trúc điều khiển (if/else) và vòng lặp (for/while)

**Tháng 1 – Tuần 1** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Điều khiển luồng chương trình bằng điều kiện.
- Lặp lại thao tác bằng `for` và `while` — nền tảng để sau này lặp qua danh sách test case, test data.

## 📘 Nội dung học

1. **Câu lệnh điều kiện**: `if`/`elif`/`else` cho phép chương trình "rẽ nhánh" — chỉ chạy 1 khối lệnh nếu điều kiện đúng. Đây chính là cách 1 bài test tự động quyết định "PASS hay FAIL".

   ```python
   status_code = 404
   if status_code == 200:
       print("Test PASS: API tra ve thanh cong")
   elif status_code == 404:
       print("Test FAIL: khong tim thay resource")
   else:
       print("Test FAIL: loi khong xac dinh")
   ```

2. **Vòng lặp `for`**: lặp qua 1 dãy giá trị có sẵn — dùng `range(n)` để lặp n lần theo số, hoặc lặp trực tiếp qua từng phần tử của chuỗi/list. Sau này bạn sẽ dùng `for` để chạy lần lượt qua từng test case trong 1 danh sách test data.

   ```python
   test_cases = ["login hop le", "login sai password", "login bo trong username"]
   for case in test_cases:
       print(f"Dang chay: {case}")
   ```

3. **Vòng lặp `while`**: lặp lại khi 1 điều kiện còn đúng, dừng khi điều kiện sai — phải luôn có bước làm điều kiện tiến gần tới chỗ dừng, nếu không sẽ chạy vô hạn (treo chương trình).

   ```python
   so_lan_thu = 0
   thanh_cong = False
   while so_lan_thu < 3 and not thanh_cong:
       so_lan_thu += 1
       print(f"Thu lai lan {so_lan_thu}")
       # gia lap: lan thu thu 2 thi thanh cong
       if so_lan_thu == 2:
           thanh_cong = True
   ```

4. **Điều khiển vòng lặp**: `break` thoát hẳn vòng lặp ngay lập tức, `continue` bỏ qua phần còn lại của lượt lặp hiện tại và nhảy sang lượt kế tiếp, `pass` là lệnh "không làm gì cả" dùng để giữ chỗ khi cú pháp bắt buộc phải có 1 khối lệnh.

   ```python
   for so in range(1, 11):
       if so % 2 != 0:
           continue          # bo qua so le
       if so == 8:
           break              # dung han vong lap khi gap so 8
       print(so)              # in ra: 2, 4, 6
   ```

5. **Liên hệ thực tế QA**: dùng vòng lặp để chạy lại 1 hành động (vd retry click khi phần tử chưa kịp hiển thị) hoặc kiểm tra toàn bộ danh sách phần tử trên UI (vd duyệt qua tất cả sản phẩm trong giỏ hàng để assert từng dòng đúng giá).

   ```python
   gio_hang = [{"ten": "Ao thun", "gia": 100}, {"ten": "Quan jean", "gia": 250}]
   for san_pham in gio_hang:
       assert san_pham["gia"] > 0, f"San pham {san_pham['ten']} co gia khong hop le"
   print("Tat ca san pham deu co gia hop le")
   ```

## 📚 Tài liệu tham khảo
- [Python.org – More Control Flow Tools](https://docs.python.org/3/tutorial/controlflow.html)
- [W3Schools – Python If...Else](https://www.w3schools.com/python/python_conditions.asp)
- [W3Schools – Python For Loops](https://www.w3schools.com/python/python_for_loops.asp) / [While Loops](https://www.w3schools.com/python/python_while_loops.asp)
- Luyện tập online: [HackerRank – Python (Easy)](https://www.hackerrank.com/domains/python)

## ✍️ Bài tập
1. Viết chương trình kiểm tra 1 số nhập vào là số nguyên tố hay không.
2. Viết chương trình tính giai thừa của n (n nhập từ bàn phím) bằng vòng lặp.
3. Viết chương trình đảo ngược 1 chuỗi (không dùng slicing `[::-1]`, dùng vòng lặp).
4. Viết chương trình in ra các số chẵn từ 1 đến 100, dùng `continue` để bỏ qua số lẻ.
5. Viết chương trình đoán số: máy chọn ngẫu nhiên 1 số từ 1-100 (`import random`), người dùng nhập số đoán, chương trình lặp và gợi ý "quá lớn/quá nhỏ" đến khi đoán đúng thì `break`.
