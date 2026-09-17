# Bài 18: Tự động hóa API Testing với `requests` + Pytest

**Tháng 2 – Tuần 8** | Thời lượng gợi ý: 2 ngày + 1 ngày bài tập tổng hợp tháng 2

## 🎯 Mục tiêu
- Chuyển từ test API bằng tay (Postman) sang tự động hóa bằng code — JD ghi rõ *"kinh nghiệm kiểm thử API tự động là một lợi thế"*.

## 📘 Nội dung học
1. **Thư viện `requests`**: là thư viện Python phổ biến nhất để gọi HTTP request bằng code — mỗi method (`get/post/put/delete`) tương ứng đúng 1 HTTP method đã học ở Bài 17. `params` truyền query param, `json` truyền body dạng JSON, `headers` truyền các header cần thiết (vd token xác thực).

   ```python
   import requests

   # GET với query param
   response = requests.get("https://reqres.in/api/users", params={"page": 2})

   # POST với body JSON
   response = requests.post(
       "https://reqres.in/api/users",
       json={"name": "Tuan", "job": "QA Automation Engineer"},
       headers={"Content-Type": "application/json"},
   )
   ```

2. **Đọc response**: object `response` trả về từ `requests` chứa mọi thông tin cần kiểm tra — mã trạng thái, dữ liệu, header, và cả thời gian phản hồi.

   ```python
   print(response.status_code)                 # 201
   print(response.json())                       # dict: {'name': 'Tuan', 'job': '...', 'id': '123', ...}
   print(response.headers["Content-Type"])      # application/json; charset=utf-8
   print(response.elapsed.total_seconds())      # 0.284 (giây) -> dùng để kiểm tra hiệu năng cơ bản
   ```

3. **Kết hợp với Pytest**: viết test API hoàn toàn theo đúng chuẩn `test_*.py` đã học ở Bài 13-14 — chỉ khác là dùng `requests` thay vì Playwright `page`, và `parametrize` giúp test nhiều id/input khác nhau chỉ với 1 hàm.

   ```python
   import pytest
   import requests

   def test_get_danh_sach_user():
       response = requests.get("https://reqres.in/api/users?page=2")
       assert response.status_code == 200
       assert isinstance(response.json()["data"], list)
       assert len(response.json()["data"]) > 0

   @pytest.mark.parametrize("user_id,expected_status", [
       (2, 200),
       (9999, 404),   # id không tồn tại -> mong đợi 404
   ])
   def test_get_user_theo_id(user_id, expected_status):
       response = requests.get(f"https://reqres.in/api/users/{user_id}")
       assert response.status_code == expected_status
   ```

4. **Fixture cho API**: tương tự tinh thần fixture `page` của Playwright ở Bài 13 — thay vì gõ lại `base_url` trong từng test, khai báo 1 lần trong fixture (đặt ở `conftest.py` để dùng chung toàn bộ file test API).

   ```python
   # conftest.py
   import pytest

   @pytest.fixture(scope="session")
   def api_base_url():
       return "https://reqres.in/api"

   # test_api_users.py
   def test_get_user(api_base_url):
       response = requests.get(f"{api_base_url}/users/2")
       assert response.status_code == 200
       assert response.json()["data"]["id"] == 2
   ```

## 📚 Tài liệu tham khảo
- [Requests Docs – Quickstart](https://requests.readthedocs.io/en/latest/user/quickstart/)
- [Real Python – Python's Requests Library](https://realpython.com/python-requests/)
- API demo: [reqres.in](https://reqres.in), [jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com)

## ✍️ Bài tập
1. Viết file `test_api_users.py`: test `GET /api/users?page=2` từ reqres.in, assert `status_code == 200`, assert response có field `data` là 1 list không rỗng.
2. Viết test `POST /api/users` tạo user mới, assert status code `201`, assert response chứa đúng `name`/`job` đã gửi lên.
3. Viết test kiểm tra response time: assert `response.elapsed.total_seconds() < 2` (mô phỏng kiểm tra hiệu năng cơ bản).
4. Dùng `parametrize` viết 5 test case cho `GET /api/users/{id}` với các id khác nhau (bao gồm 1 id không tồn tại để kiểm tra status `404`).
5. **Bài tập tổng hợp tháng 2**: hoàn thiện 1 bộ test tự động (UI qua Playwright + API qua requests) cho 1 luồng nghiệp vụ hoàn chỉnh mà bạn tự chọn, tối thiểu 10 test case, cấu trúc POM rõ ràng, chạy ra report HTML — đây sẽ là nền cho Portfolio Project ở tháng 3.
