# Bài 16: Test Report — pytest-html / Allure Report

**Tháng 2 – Tuần 7** | Thời lượng gợi ý: 2 ngày + 1 ngày review code

## 🎯 Mục tiêu
- Xuất báo cáo test rõ ràng — đúng yêu cầu JD *"chuẩn bị các báo cáo thực hiện kiểm thử rõ ràng và truyền đạt các rủi ro..."*. Report cũng là thứ bạn sẽ đính kèm vào portfolio project ở tháng 3.

## 📘 Nội dung học
1. **`pytest-html`**: là plugin đơn giản nhất để ra report — chỉ cần thêm 2 cờ vào lệnh `pytest`, không cần cấu hình gì thêm, phù hợp để bắt đầu.

   ```bash
   pip install pytest-html
   pytest --html=report.html --self-contained-html
   ```
   Kết quả: 1 file `report.html` duy nhất (mở trực tiếp bằng trình duyệt) liệt kê từng test PASS/FAIL, thời gian chạy, và log lỗi nếu có.

2. **Allure Report** (nâng cao hơn, đẹp và chi tiết hơn): khác `pytest-html` ở chỗ Allure cho phép gắn **từng bước** (step) bên trong 1 test, giúp report đọc như 1 kịch bản test thật sự thay vì chỉ PASS/FAIL chung chung.

   ```python
   import allure

   @allure.title("Đăng nhập thành công với tài khoản hợp lệ")
   def test_login_thanh_cong(page):
       with allure.step("Mở trang saucedemo"):
           page.goto("https://www.saucedemo.com")
       with allure.step("Nhập username và password hợp lệ"):
           page.get_by_placeholder("Username").fill("standard_user")
           page.get_by_placeholder("Password").fill("secret_sauce")
       with allure.step("Click nút Login và kiểm tra vào đúng trang Products"):
           page.get_by_text("Login").click()
           expect(page.locator(".title")).to_have_text("Products")
   ```
   ```bash
   pip install allure-pytest
   pytest --alluredir=allure-results
   allure serve allure-results   # mở report dạng web, thấy rõ từng step pass/fail
   ```

3. **Chụp screenshot khi test fail**: `pytest-playwright` hỗ trợ sẵn cờ dòng lệnh để tự động lưu ảnh chụp màn hình (và cả video) đúng thời điểm test fail — không cần viết thêm code, cực hữu ích khi cần đính kèm bằng chứng vào báo cáo lỗi (đúng JD *"chuẩn bị báo cáo kiểm thử rõ ràng"*).

   ```bash
   pytest --screenshot=only-on-failure --video=retain-on-failure
   ```
   Sau khi chạy, các file `.png`/`.webm` sẽ được lưu trong thư mục `test-results/` — mở lên xem đúng khoảnh khắc test fail trên trình duyệt.

4. **Review code & docstring**: dọn dẹp lại toàn bộ code đã viết tuần 5-7, thêm mô tả ngắn cho class/method (giống Bài 03 đã học) để người khác đọc code hiểu ngay mục đích mà không cần đọc hết logic bên trong.

   ```python
   class CartPage(BasePage):
       """Trang giỏ hàng của saucedemo — quản lý các thao tác thêm/xóa sản phẩm."""

       def add_product(self, product_name: str):
           """Thêm 1 sản phẩm vào giỏ hàng theo tên hiển thị trên trang."""
           self.page.get_by_text(product_name).locator("..").get_by_text("Add to cart").click()
   ```

## 📚 Tài liệu tham khảo
- [pytest-html – PyPI docs](https://pytest-html.readthedocs.io/en/latest/)
- [Allure Report – Pytest integration](https://allurereport.org/docs/pytest/)
- [Playwright Docs – Pytest plugin: screenshots & videos](https://playwright.dev/python/docs/test-runners#configuring-browsers)

## ✍️ Bài tập
1. Chạy toàn bộ bộ test hiện có với `pytest --html=report.html --self-contained-html`, mở file HTML xem kết quả.
2. Cài Allure, chạy test ra kết quả Allure (`pytest --alluredir=allure-results` rồi `allure serve allure-results`), so sánh trải nghiệm với pytest-html.
3. Bật cấu hình chụp screenshot khi fail, cố tình cho 1 test fail (vd đổi sai locator) để xem screenshot được lưu lại thế nào.
4. Viết docstring cho toàn bộ class trong `pages/` (mỗi class 1-2 dòng mô tả, mỗi method 1 dòng).
5. **Review & dọn dẹp**: đọc lại toàn bộ code tuần 5-7 như 1 người review — đặt tên biến/hàm rõ nghĩa hơn nếu cần, xóa code thừa, đảm bảo `pytest` chạy xanh 100%.
