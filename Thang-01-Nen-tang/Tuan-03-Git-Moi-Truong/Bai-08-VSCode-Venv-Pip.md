# Bài 08: VSCode + Virtual Environment (venv) + pip

**Tháng 1 – Tuần 3** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Thiết lập môi trường làm việc chuẩn như dân automation thật sự dùng: mỗi project 1 môi trường ảo riêng, quản lý thư viện qua `requirements.txt`.

## 📘 Nội dung học

1. **VSCode nâng cao**: cài thêm extension "Python" và "Pylance" (Microsoft, gợi ý code + kiểm tra lỗi ngay khi gõ), "GitLens" (xem lịch sử thay đổi từng dòng code ngay trong editor). **Debug** cho phép chạy code từng bước và xem giá trị biến thay đổi ra sao — hữu ích hơn nhiều so với chỉ dùng `print()` để dò lỗi.

   *Ví dụ debug:* mở file `.py`, click vào lề trái 1 dòng để đặt **breakpoint** (chấm đỏ), nhấn `F5` để chạy debug — chương trình sẽ dừng lại đúng dòng đó, bạn xem được giá trị mọi biến hiện tại ở panel "Variables" trước khi cho chạy tiếp (`F5` lần nữa hoặc `F10` để chạy từng dòng).

2. **Virtual environment (`venv`)**: là 1 "môi trường Python riêng biệt" cho từng project, không dùng chung thư viện với project khác hay với Python cài trên toàn máy — tránh trường hợp project A cần `requests` bản 2.0 còn project B cần bản 3.0, cài chung sẽ xung đột.

   ```bash
   python -m venv venv                    # tao moi truong ao ten "venv"

   # Kich hoat:
   venv\Scripts\activate                  # Windows
   source venv/bin/activate               # Mac/Linux

   # Sau khi kich hoat, dong lenh se hien "(venv)" o dau -> dang o trong moi truong ao
   ```

3. **`pip`**: công cụ cài đặt thư viện Python. `pip install <ten>` cài 1 thư viện vào venv đang active, `pip freeze` liệt kê chính xác các thư viện + version đang cài (ghi ra file `requirements.txt` để chia sẻ cho người khác/CI cài lại y hệt).

   ```bash
   pip install requests pytest-playwright
   pip freeze > requirements.txt          # xuat danh sach thu vien + version

   # tren may khac (hoac tren CI/CD), cai lai y het bang:
   pip install -r requirements.txt
   ```
   *Ví dụ nội dung `requirements.txt`:*
   ```text
   requests==2.31.0
   pytest-playwright==0.4.4
   ```

4. **Cấu trúc project chuẩn ban đầu**: mỗi project automation nên có 1 folder riêng, chứa `venv/` (môi trường ảo — không commit lên Git), `requirements.txt` (danh sách thư viện — có commit), và `.gitignore` nhớ loại trừ `venv/` ra khỏi Git (vì venv rất nặng và có thể tạo lại bất cứ lúc nào từ `requirements.txt`).

   ```text
   qa-practice/
   ├── venv/                 # KHONG commit (co trong .gitignore)
   ├── requirements.txt      # CO commit — de nguoi khac cai lai dung version
   ├── .gitignore
   └── test_login.py
   ```

## 📚 Tài liệu tham khảo
- [Python.org – venv](https://docs.python.org/3/library/venv.html)
- [Real Python – Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/)
- [VSCode Docs – Python in VSCode](https://code.visualstudio.com/docs/python/python-tutorial)

## ✍️ Bài tập
1. Tạo 1 folder project mới `qa-practice/`, tạo virtual environment, kích hoạt thành công (thấy `(venv)` trước dòng lệnh).
2. Cài thử thư viện `requests` trong venv, viết 1 file `.py` import `requests` và chạy thử `requests.get("https://reqres.in/api/users")`, in ra `response.status_code`.
3. Xuất `requirements.txt`, xóa venv, tạo lại venv mới và cài lại bằng `pip install -r requirements.txt` để chắc chắn hiểu quy trình.
4. Cấu hình VSCode để chạy/debug được file Python (đặt 1 breakpoint, chạy debug F5, quan sát giá trị biến).
