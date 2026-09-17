# Bài 08: VSCode + Virtual Environment (venv) + pip

**Tháng 1 – Tuần 3** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Thiết lập môi trường làm việc chuẩn như dân automation thật sự dùng: mỗi project 1 môi trường ảo riêng, quản lý thư viện qua `requirements.txt`.

## 📘 Nội dung học
1. **VSCode nâng cao**: extension hữu ích (Python, Pylance, GitLens, Even Better TOML), debug cơ bản (đặt breakpoint, F5 chạy debug).
2. **Virtual environment (`venv`)**: vì sao cần môi trường ảo riêng cho từng project (tránh xung đột version thư viện).
   - Tạo: `python -m venv venv`
   - Kích hoạt: `venv\Scripts\activate` (Windows) / `source venv/bin/activate` (Mac/Linux)
3. **`pip`**: cài thư viện `pip install <ten-thu-vien>`, xuất danh sách thư viện `pip freeze > requirements.txt`, cài lại từ file `pip install -r requirements.txt`.
4. Cấu trúc project chuẩn ban đầu: 1 folder project riêng, có `venv/`, `requirements.txt`, `.gitignore` (nhớ ignore `venv/`).

## 📚 Tài liệu tham khảo
- [Python.org – venv](https://docs.python.org/3/library/venv.html)
- [Real Python – Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/)
- [VSCode Docs – Python in VSCode](https://code.visualstudio.com/docs/python/python-tutorial)

## ✍️ Bài tập
1. Tạo 1 folder project mới `qa-practice/`, tạo virtual environment, kích hoạt thành công (thấy `(venv)` trước dòng lệnh).
2. Cài thử thư viện `requests` trong venv, viết 1 file `.py` import `requests` và chạy thử `requests.get("https://reqres.in/api/users")`, in ra `response.status_code`.
3. Xuất `requirements.txt`, xóa venv, tạo lại venv mới và cài lại bằng `pip install -r requirements.txt` để chắc chắn hiểu quy trình.
4. Cấu hình VSCode để chạy/debug được file Python (đặt 1 breakpoint, chạy debug F5, quan sát giá trị biến).
