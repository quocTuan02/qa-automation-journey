# Bài 04: List, Tuple, Dict, Set nâng cao + xử lý String

**Tháng 1 – Tuần 2** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Thao tác thành thạo với các cấu trúc dữ liệu — đây là kiểu dữ liệu bạn sẽ dùng liên tục để lưu test data, danh sách locator, kết quả test.

## 📘 Nội dung học

1. **List**: là danh sách có thứ tự, có thể sửa/thêm/xóa phần tử. `indexing` (`list[0]`) lấy 1 phần tử theo vị trí, `slicing` (`list[1:3]`) cắt ra 1 đoạn con. **List comprehension** là cách viết gọn 1 vòng lặp tạo list mới chỉ trong 1 dòng — cực hay dùng để lọc dữ liệu test.

   ```python
   test_case_ids = [1, 2, 3, 4, 5, 6, 7, 8]
   test_case_ids.append(9)              # them phan tu vao cuoi
   test_case_ids.remove(3)              # xoa gia tri 3

   # List comprehension: loc ra cac id la so chan
   id_chan = [tc_id for tc_id in test_case_ids if tc_id % 2 == 0]
   print(id_chan)   # [2, 4, 6, 8]
   ```

2. **Tuple**: giống list nhưng bất biến (immutable) — sau khi tạo không sửa được nữa. Dùng tuple khi dữ liệu không nên bị thay đổi trong lúc chương trình chạy (vd 1 bộ tọa độ, 1 cặp kết quả cố định).

   ```python
   ket_qua_mong_doi = (200, "OK")   # tuple: status_code va message khong the sua nham
   status, message = ket_qua_mong_doi  # unpack tuple ra 2 bien
   print(status, message)              # 200 OK
   ```

3. **Dict**: lưu dữ liệu theo cặp key-value (giống 1 bảng tra cứu), truy cập nhanh theo key thay vì phải dò từng phần tử như list. `.get()` lấy giá trị an toàn (không lỗi nếu key không tồn tại), `.items()` cho phép duyệt cả key lẫn value cùng lúc.

   ```python
   test_account = {"username": "standard_user", "password": "secret_sauce", "role": "admin"}

   print(test_account.get("username"))          # standard_user
   print(test_account.get("email", "N/A"))       # "N/A" vi key "email" khong ton tai

   for key, value in test_account.items():
       print(f"{key}: {value}")
   ```

4. **Set**: tập hợp không cho phép phần tử trùng lặp, hỗ trợ các phép toán tập hợp như hợp (`|`), giao (`&`) — hữu ích khi so sánh 2 tập dữ liệu test (vd so sánh danh sách user mong đợi với danh sách user thực tế trả về từ API).

   ```python
   user_mong_doi = {"alice", "bob", "carol"}
   user_thuc_te = {"alice", "carol", "dave"}

   print(user_mong_doi & user_thuc_te)   # {'alice', 'carol'} -> giao nhau
   print(user_mong_doi - user_thuc_te)   # {'bob'} -> thieu trong thuc te (bug!)
   ```

5. **Xử lý string**: `split()` cắt chuỗi thành list theo ký tự phân cách, `join()` làm ngược lại (ghép list thành chuỗi), `strip()` xóa khoảng trắng thừa ở đầu/cuối (rất hay dùng khi đọc dữ liệu test từ file có khoảng trắng lạc), `replace()` thay thế đoạn text, toán tử `in` kiểm tra 1 chuỗi con có nằm trong chuỗi lớn không.

   ```python
   dong_csv = "  standard_user, secret_sauce, admin  \n"
   dong_sach = dong_csv.strip()                 # xoa khoang trang/xuong dong thua
   cac_truong = dong_sach.split(",")            # ['standard_user', ' secret_sauce', ' admin']
   cac_truong = [f.strip() for f in cac_truong] # xoa khoang trang tung phan tu

   print(cac_truong)                            # ['standard_user', 'secret_sauce', 'admin']
   print("admin" in cac_truong)                 # True
   print(", ".join(cac_truong))                  # noi lai thanh chuoi: "standard_user, secret_sauce, admin"
   ```

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
