# Bài 18: Tự động hóa API Testing với `requests` + Pytest

**Tháng 2 – Tuần 8** | Thời lượng gợi ý: 2 ngày + 1 ngày bài tập tổng hợp tháng 2

## 🎯 Mục tiêu
- Chuyển từ test API bằng tay (Postman) sang tự động hóa bằng code — JD ghi rõ *"kinh nghiệm kiểm thử API tự động là một lợi thế"*.

## 📘 Nội dung học
1. **Thư viện `requests`**: `requests.get()/post()/put()/delete()`, truyền `params`, `json`, `headers`.
2. **Đọc response**: `.status_code`, `.json()`, `.headers`, `.elapsed.total_seconds()` (đo response time).
3. **Kết hợp với Pytest**: viết test API theo đúng chuẩn `test_*.py` như đã học ở Bài 13-14, dùng `assert` để kiểm tra status code, dữ liệu trả về, dùng `parametrize` để test nhiều bộ input.
4. **Fixture cho API**: fixture trả về `base_url` hoặc `session` requests dùng chung cho các test (tương tự tinh thần fixture `page` của Playwright).

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
