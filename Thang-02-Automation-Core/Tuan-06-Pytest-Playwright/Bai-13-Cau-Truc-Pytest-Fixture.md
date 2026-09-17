# Bài 13: Cấu trúc Pytest — test function, fixture, conftest.py

**Tháng 2 – Tuần 6** | Thời lượng gợi ý: 2-3 ngày

## 🎯 Mục tiêu
- Chuyển từ "viết script chạy 1 lần" sang "viết bộ test có tổ chức" bằng Pytest — framework test đứng trong JD (`Pytest`) và là chuẩn để chạy tự động trong CI/CD sau này.

## 📘 Nội dung học
1. **Quy ước Pytest**: Pytest tự động tìm và chạy test dựa theo tên file/hàm, không cần đăng ký thủ công — chỉ cần file bắt đầu bằng `test_` (hoặc kết thúc `_test.py`) và hàm bắt đầu bằng `def test_`. Chạy toàn bộ bằng lệnh `pytest`.

   ```python
   # file: test_sample.py
   def test_cong_hai_so():
       ket_qua = 2 + 3
       assert ket_qua == 5

   def test_tru_hai_so():
       assert 10 - 4 == 6
   ```
   ```bash
   pytest -v          # chạy tất cả test, in chi tiết từng test PASS/FAIL
   pytest test_sample.py::test_cong_hai_so   # chỉ chạy 1 test cụ thể
   ```

2. **`assert` trong Pytest**: chỉ cần dùng từ khóa `assert` có sẵn của Python — không cần học API assert riêng như nhiều framework khác. Điểm mạnh: khi assert fail, Pytest tự in ra chi tiết giá trị 2 bên để so sánh, giúp debug nhanh hơn nhiều so với `assert` chạy tay.

   ```python
   def test_login_thanh_cong():
       tieu_de_thuc_te = "Product"
       assert tieu_de_thuc_te == "Products"   # sẽ FAIL và Pytest in rõ: "Product" != "Products"
   ```

3. **Fixture (`@pytest.fixture`)**: là hàm chuẩn bị sẵn dữ liệu/trạng thái trước khi test chạy (setup) và có thể dọn dẹp sau khi test xong (teardown) — thay vì lặp lại đoạn code "mở browser, đăng nhập..." ở đầu mọi hàm test, viết 1 lần trong fixture rồi mọi test chỉ cần khai báo tên fixture làm tham số là dùng được.

   ```python
   import pytest

   @pytest.fixture
   def base_url():
       return "https://www.saucedemo.com"

   def test_mo_trang(page, base_url):   # Pytest tự "tiêm" giá trị fixture vào tham số cùng tên
       page.goto(base_url)
       assert page.title() != ""
   ```

4. **`conftest.py`**: là file đặc biệt Pytest tự động nhận diện — fixture khai báo ở đây dùng được cho **mọi** file test trong cùng thư mục (và thư mục con), không cần import thủ công.

   ```python
   # conftest.py
   import pytest

   @pytest.fixture
   def valid_credentials():
       return {"username": "standard_user", "password": "secret_sauce"}
   ```
   ```python
   # test_login.py — dùng thẳng fixture từ conftest.py, không cần import
   def test_login_hop_le(page, valid_credentials):
       page.goto("https://www.saucedemo.com")
       page.get_by_placeholder("Username").fill(valid_credentials["username"])
       page.get_by_placeholder("Password").fill(valid_credentials["password"])
       page.get_by_text("Login").click()
   ```

5. **`pytest-playwright` plugin**: khi cài `pytest-playwright`, bạn có ngay fixture `page` (và `browser`, `context`) mà không cần tự viết `sync_playwright()`, `browser.launch()`, `browser.close()` như Bài 11 — plugin tự lo việc mở/đóng browser trước/sau mỗi test.

   ```python
   def test_dung_fixture_page_co_san(page):   # "page" o day la fixture co san, khong can tu tao
       page.goto("https://www.saucedemo.com")
       expect(page).to_have_title("Swag Labs")
   ```

## 📚 Tài liệu tham khảo
- [Pytest Docs – Get Started](https://docs.pytest.org/en/stable/getting-started.html)
- [Pytest Docs – Fixtures](https://docs.pytest.org/en/stable/how-to/fixtures.html)
- [Playwright Docs – Pytest plugin](https://playwright.dev/python/docs/test-runners)

## ✍️ Bài tập
1. Cài `pytest-playwright`, chuyển script login (bài 12) từ file `.py` chạy tay sang file `test_login.py` chuẩn Pytest, chạy bằng lệnh `pytest -v`.
2. Viết 1 fixture riêng trong `conftest.py` để trả về URL base của trang test (vd `https://www.saucedemo.com`), dùng lại fixture này ở nhiều test.
3. Viết 3 test case độc lập cho luồng login: (1) login đúng, (2) sai password, (3) bỏ trống username — mỗi case 1 hàm `test_...` riêng.
4. Thử chạy `pytest --headed` và `pytest --browser firefox` để hiểu cách `pytest-playwright` cho phép cấu hình qua command line.
