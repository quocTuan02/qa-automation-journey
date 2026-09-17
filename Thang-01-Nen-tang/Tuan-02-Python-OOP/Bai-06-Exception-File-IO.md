# Bài 06: Exception Handling & Đọc/ghi file (CSV, JSON)

**Tháng 1 – Tuần 2** | Thời lượng gợi ý: 2 ngày + 1 ngày bài tập tổng hợp

## 🎯 Mục tiêu
- Xử lý lỗi không làm crash chương trình — automation script chạy hàng loạt test cần biết bắt lỗi để không dừng cả bộ test khi 1 case fail.
- Đọc/ghi file CSV, JSON — 2 định dạng phổ biến nhất để lưu test data.

## 📘 Nội dung học

1. **`try / except / else / finally`**: `try` bao quanh đoạn code có nguy cơ lỗi, `except` bắt lỗi và xử lý thay vì để chương trình crash, `else` chạy khi không có lỗi xảy ra, `finally` luôn chạy dù có lỗi hay không (thường dùng để dọn dẹp, vd đóng file/kết nối). Nên bắt lỗi **cụ thể** (`except ValueError:`) thay vì bắt chung chung (`except Exception:`) để không vô tình nuốt mất lỗi khác không lường trước.

   ```python
   def chia(a, b):
       try:
           ket_qua = a / b
       except ZeroDivisionError:
           print("Loi: khong the chia cho 0")
           return None
       except ValueError:
           print("Loi: du lieu nhap khong hop le")
           return None
       else:
           print("Chia thanh cong, khong co loi")
           return ket_qua
       finally:
           print("Da xu ly xong phep chia")   # luon chay du co loi hay khong

   print(chia(10, 2))   # 5.0
   print(chia(10, 0))   # None, kem thong bao loi
   ```

2. **`raise`**: tự tạo và "ném" ra 1 lỗi khi phát hiện dữ liệu/trạng thái không hợp lệ — hữu ích khi viết hàm kiểm tra dữ liệu test, muốn báo lỗi rõ ràng thay vì để chương trình chạy tiếp với dữ liệu sai.

   ```python
   def kiem_tra_tuoi(tuoi):
       if tuoi < 0:
           raise ValueError(f"Tuoi khong hop le: {tuoi}")
       return tuoi

   try:
       kiem_tra_tuoi(-5)
   except ValueError as e:
       print(f"Bat duoc loi: {e}")   # Bat duoc loi: Tuoi khong hop le: -5
   ```

3. **Đọc/ghi file text** cơ bản: dùng `with open(...) as f:` để mở file — cách này tự động đóng file lại sau khi dùng xong, kể cả khi có lỗi xảy ra giữa chừng (an toàn hơn tự gọi `open()`/`close()` tay).

   ```python
   with open("ket_qua_test.txt", "w") as f:
       f.write("Test login: PASS\n")
       f.write("Test cart: PASS\n")

   with open("ket_qua_test.txt", "r") as f:
       noi_dung = f.read()
       print(noi_dung)
   ```

4. **Module `csv`**: `csv.DictReader` đọc file CSV và trả về từng dòng dưới dạng dict (key là tên cột) — rất tiện để đọc test data có nhiều cột. `csv.writer` dùng để ghi dữ liệu ra file CSV.

   ```python
   import csv

   # Gia su file test_data.csv co noi dung:
   # username,password,role
   # standard_user,secret_sauce,admin
   # locked_out_user,secret_sauce,user

   with open("test_data.csv", "r") as f:
       reader = csv.DictReader(f)
       for row in reader:
           print(row["username"], "-", row["role"])
   ```

5. **Module `json`**: `json.loads()`/`json.load()` chuyển chuỗi/file JSON thành dict Python để xử lý; `json.dumps()`/`json.dump()` làm ngược lại. Cực kỳ quan trọng vì response của mọi API (sẽ học ở Tháng 2) đều trả về dạng JSON.

   ```python
   import json

   # Mo phong 1 response API dang chuoi JSON
   response_text = '{"id": 1, "name": "Ao thun", "price": 100}'
   data = json.loads(response_text)          # chuyen chuoi JSON -> dict Python
   print(data["name"], data["price"])         # Ao thun 100

   # Ghi dict Python ra file JSON
   with open("san_pham.json", "w") as f:
       json.dump(data, f, indent=2)
   ```

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
