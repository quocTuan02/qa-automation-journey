# Bài 15: Page Object Model (POM) — khái niệm và refactor

**Tháng 2 – Tuần 7** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Nắm được pattern thiết kế **bắt buộc** của mọi automation framework chuyên nghiệp, đúng như JD mô tả *"phát triển, duy trì và thực thi kịch bản kiểm thử tự động"* — muốn "duy trì" được thì code phải có cấu trúc, không viết dồn hết vào 1 file test.

## 📘 Nội dung học
1. **Vấn đề khi không có POM**: khi locator được viết trực tiếp trong từng file test, cùng 1 phần tử (vd nút "Login") có thể xuất hiện lặp lại ở 5-10 file test khác nhau. Chỉ cần dev đổi 1 attribute HTML là toàn bộ các chỗ đó đều fail, và bạn phải tìm sửa từng nơi — rất dễ sót.

   ```python
   # ❌ Không có POM: locator lặp lại trong từng file test
   # test_login.py
   def test_login(page):
       page.get_by_placeholder("Username").fill("standard_user")
       page.get_by_placeholder("Password").fill("secret_sauce")
       page.get_by_text("Login").click()

   # test_login_negative.py — locator giống hệt bị copy lại
   def test_login_sai_password(page):
       page.get_by_placeholder("Username").fill("standard_user")
       page.get_by_placeholder("Password").fill("sai_password")
       page.get_by_text("Login").click()
   ```

2. **Khái niệm POM**: mỗi trang web tương ứng với 1 `class` (dùng lại kiến thức OOP ở Bài 05) — locator và hành động trên trang đó được gói gọn thành **method** của class, file test chỉ còn gọi method chứ không chứa locator nào cả. Khi HTML đổi, chỉ cần sửa 1 chỗ duy nhất trong class.

   ```python
   # ✅ Có POM: locator chỉ khai báo 1 lần trong class
   class LoginPage:
       def __init__(self, page):
           self.page = page
           self.username_input = page.get_by_placeholder("Username")
           self.password_input = page.get_by_placeholder("Password")
           self.login_button = page.get_by_text("Login")

       def login(self, username, password):
           self.username_input.fill(username)
           self.password_input.fill(password)
           self.login_button.click()
   ```
   ```python
   # test_login.py — giờ chỉ gọi method, không còn 1 locator nào trong file test
   def test_login(page):
       login_page = LoginPage(page)
       login_page.login("standard_user", "secret_sauce")
   ```

3. **Cấu trúc thư mục chuẩn**:
   ```
   project/
   ├── pages/
   │   ├── base_page.py      # class cha chung (vd navigate, wait chung)
   │   ├── login_page.py
   │   └── cart_page.py
   ├── tests/
   │   ├── test_login.py
   │   └── test_cart.py
   ├── conftest.py
   └── requirements.txt
   ```

4. **`BasePage`**: là class cha chứa các hành vi/attribute mà **mọi** page đều cần (vd lưu lại `page`, method điều hướng chung) — các page cụ thể (`LoginPage`, `CartPage`) kế thừa từ `BasePage` để không phải viết lại `__init__` giống nhau ở mọi class.

   ```python
   # base_page.py
   class BasePage:
       def __init__(self, page):
           self.page = page

       def go_to(self, url):
           self.page.goto(url)

   # login_page.py
   from pages.base_page import BasePage

   class LoginPage(BasePage):
       def __init__(self, page):
           super().__init__(page)         # gọi __init__ của BasePage để lưu self.page
           self.username_input = page.get_by_placeholder("Username")
           self.password_input = page.get_by_placeholder("Password")
           self.login_button = page.get_by_text("Login")

       def login(self, username, password):
           self.go_to("https://www.saucedemo.com")   # dùng lại method từ BasePage
           self.username_input.fill(username)
           self.password_input.fill(password)
           self.login_button.click()
   ```

5. **Refactor**: chuyển code tuần 5-6 (đang viết locator trực tiếp trong file test) sang đúng cấu trúc trên — mục tiêu cuối: mở bất kỳ file trong `tests/` cũng không thấy 1 dòng `page.locator(...)` hay `get_by_...` nào, tất cả nằm trong `pages/`.

## 📚 Tài liệu tham khảo
- [Playwright Docs – Page Object Models](https://playwright.dev/python/docs/pom)
- [Martin Fowler – PageObject](https://martinfowler.com/bliki/PageObject.html) (bài gốc định nghĩa pattern này)
- [Real Python – OOP recap](https://realpython.com/python3-object-oriented-programming/) (ôn lại nếu cần trước khi refactor)

## ✍️ Bài tập
1. Tạo cấu trúc thư mục `pages/` và `tests/` như trên cho project saucedemo hiện có.
2. Viết `base_page.py` với class `BasePage` chứa `__init__(self, page)` lưu lại `page`.
3. Viết `login_page.py` với class `LoginPage(BasePage)`: locator username/password/login button ở `__init__` hoặc property, method `login(username, password)`.
4. Viết `cart_page.py` tương tự cho trang giỏ hàng: method `add_product(name)`, method `get_cart_items()`.
5. Refactor toàn bộ test tuần 6 (`test_login.py`, `test_cart.py`) để chỉ gọi method từ các Page class — không còn locator nào nằm trực tiếp trong file test.
