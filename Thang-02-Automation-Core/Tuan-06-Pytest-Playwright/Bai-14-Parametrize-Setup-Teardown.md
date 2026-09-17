# Bài 14: Parametrize test + Setup/Teardown nâng cao

**Tháng 2 – Tuần 6** | Thời lượng gợi ý: 2-3 ngày + 1 ngày bài tập tổng hợp

## 🎯 Mục tiêu
- Chạy 1 test với nhiều bộ dữ liệu khác nhau (data-driven testing) — kỹ năng giúp viết ít code mà cover nhiều trường hợp, đúng tinh thần "chuẩn bị test data" trong JD.

## 📘 Nội dung học
1. **`@pytest.mark.parametrize`**: thay vì copy-paste 1 hàm test nhiều lần chỉ để đổi dữ liệu đầu vào, decorator này cho phép Pytest tự chạy **cùng 1 hàm** với nhiều bộ dữ liệu khác nhau — mỗi bộ được báo cáo như 1 test riêng biệt (PASS/FAIL độc lập).

   ```python
   import pytest

   @pytest.mark.parametrize("username,password,expected_error", [
       ("", "secret_sauce", "Username is required"),
       ("standard_user", "", "Password is required"),
       ("wrong_user", "secret_sauce", "Username and password do not match"),
   ])
   def test_login_that_bai(page, username, password, expected_error):
       page.goto("https://www.saucedemo.com")
       page.get_by_placeholder("Username").fill(username)
       page.get_by_placeholder("Password").fill(password)
       page.get_by_text("Login").click()
       expect(page.locator("[data-test='error']")).to_contain_text(expected_error)
   ```
   Lệnh `pytest -v` sẽ hiển thị 3 dòng kết quả riêng biệt, mỗi dòng ứng với 1 bộ dữ liệu — dễ biết chính xác case nào fail.

2. **Fixture scope**: quyết định 1 fixture được tạo lại bao nhiêu lần. `function` (mặc định) tạo mới cho **mỗi** test — an toàn, mỗi test độc lập hoàn toàn nhưng chậm hơn (vd mở browser mới mỗi lần). `module`/`session` tạo 1 lần rồi dùng chung cho nhiều test — nhanh hơn nhưng rủi ro: test này có thể ảnh hưởng tới state của test khác nếu không cẩn thận.

   ```python
   @pytest.fixture(scope="function")   # mặc định: mỗi test 1 browser mới, an toàn
   def page_moi(browser):
       page = browser.new_page()
       yield page
       page.close()

   @pytest.fixture(scope="session")    # dùng chung 1 lần cho cả session chạy test — nhanh nhưng cẩn thận side-effect
   def api_base_url():
       return "https://reqres.in/api"
   ```

3. **Setup/Teardown nâng cao (`yield`)**: phần code **trước** `yield` chạy trước khi test thực thi (setup), giá trị sau `yield` được đưa vào test làm tham số, phần code **sau** `yield` chạy sau khi test kết thúc — dù test đó PASS hay FAIL (teardown luôn chạy).

   ```python
   @pytest.fixture
   def logged_in_page(page):
       # ---- SETUP: chạy trước test ----
       page.goto("https://www.saucedemo.com")
       page.get_by_placeholder("Username").fill("standard_user")
       page.get_by_placeholder("Password").fill("secret_sauce")
       page.get_by_text("Login").click()

       yield page   # test nhận được "page" đã login sẵn

       # ---- TEARDOWN: chạy sau test, dù pass hay fail ----
       print("Test da chay xong, don dep neu can (vd xoa du lieu test da tao)")

   def test_them_gio_hang(logged_in_page):
       logged_in_page.locator("#add-to-cart-sauce-labs-backpack").click()
       expect(logged_in_page.locator(".shopping_cart_badge")).to_have_text("1")
   ```

4. **Markers**: gắn "nhãn" cho test để chọn chạy 1 nhóm test cụ thể thay vì chạy toàn bộ — hữu ích khi bộ test lớn dần (vd chỉ chạy `smoke` test nhanh trước khi merge code, chạy `regression` đầy đủ vào ban đêm qua CI/CD).

   ```python
   @pytest.mark.smoke
   def test_login_thanh_cong(page):
       ...

   @pytest.mark.regression
   def test_them_nhieu_san_pham_vao_gio_hang(page):
       ...
   ```
   ```bash
   pytest -m smoke        # chỉ chạy các test đánh dấu @pytest.mark.smoke
   pytest -m regression   # chỉ chạy các test đánh dấu @pytest.mark.regression
   ```
   *Lưu ý:* cần khai báo marker trong `pytest.ini` hoặc `pyproject.toml` để tránh warning "unknown marker".

## 📚 Tài liệu tham khảo
- [Pytest Docs – Parametrize](https://docs.pytest.org/en/stable/how-to/parametrize.html)
- [Pytest Docs – Fixture finalization (yield)](https://docs.pytest.org/en/stable/how-to/fixtures.html#teardown-cleanup-aka-fixture-finalization)
- [Pytest Docs – Marks](https://docs.pytest.org/en/stable/how-to/mark.html)

## ✍️ Bài tập
1. Viết lại case "login sai" bằng `parametrize` với ít nhất 4 bộ dữ liệu (sai username, sai password, để trống cả 2, tài khoản bị khóa `locked_out_user` — có sẵn trên saucedemo) — assert đúng thông báo lỗi tương ứng mỗi trường hợp.
2. Viết 1 fixture `logged_in_page` dùng `yield`: setup = login vào saucedemo, sau `yield` = không cần teardown đặc biệt (Playwright tự đóng), nhưng thử thêm log "Test kết thúc" để hiểu rõ thứ tự chạy.
3. Đánh marker `@pytest.mark.smoke` cho các test quan trọng nhất (login thành công, thêm giỏ hàng), thử chạy riêng `pytest -m smoke`.
4. **Bài tập tổng hợp tuần 6**: Viết bộ test hoàn chỉnh cho luồng "thêm sản phẩm vào giỏ hàng" trên saucedemo: dùng fixture `logged_in_page`, parametrize với ít nhất 3 sản phẩm khác nhau, assert đúng tên/giá/số lượng trong giỏ hàng.
