# Bài 13: Cấu trúc Pytest — test function, fixture, conftest.py

**Tháng 2 – Tuần 6** | Thời lượng gợi ý: 2-3 ngày

## 🎯 Mục tiêu
- Chuyển từ "viết script chạy 1 lần" sang "viết bộ test có tổ chức" bằng Pytest — framework test đứng trong JD (`Pytest`) và là chuẩn để chạy tự động trong CI/CD sau này.

## 📘 Nội dung học
1. **Quy ước Pytest**: file `test_*.py`, hàm `def test_*():`, chạy bằng lệnh `pytest`.
2. **`assert` trong Pytest**: cách Pytest hiển thị lỗi rất chi tiết khi assert fail — không cần thư viện assert riêng.
3. **Fixture (`@pytest.fixture`)**: tại sao cần — dùng để chuẩn bị dữ liệu/trạng thái trước test (vd mở browser) và dọn dẹp sau test (đóng browser).
4. **`conftest.py`**: nơi đặt các fixture dùng chung cho nhiều file test.
5. **`pytest-playwright` plugin**: fixture có sẵn `page` — không cần tự viết code mở/đóng browser nữa.

## 📚 Tài liệu tham khảo
- [Pytest Docs – Get Started](https://docs.pytest.org/en/stable/getting-started.html)
- [Pytest Docs – Fixtures](https://docs.pytest.org/en/stable/how-to/fixtures.html)
- [Playwright Docs – Pytest plugin](https://playwright.dev/python/docs/test-runners)

## ✍️ Bài tập
1. Cài `pytest-playwright`, chuyển script login (bài 12) từ file `.py` chạy tay sang file `test_login.py` chuẩn Pytest, chạy bằng lệnh `pytest -v`.
2. Viết 1 fixture riêng trong `conftest.py` để trả về URL base của trang test (vd `https://www.saucedemo.com`), dùng lại fixture này ở nhiều test.
3. Viết 3 test case độc lập cho luồng login: (1) login đúng, (2) sai password, (3) bỏ trống username — mỗi case 1 hàm `test_...` riêng.
4. Thử chạy `pytest --headed` và `pytest --browser firefox` để hiểu cách `pytest-playwright` cho phép cấu hình qua command line.
