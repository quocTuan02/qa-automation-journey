# Bài 15: Page Object Model (POM) — khái niệm và refactor

**Tháng 2 – Tuần 7** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Nắm được pattern thiết kế **bắt buộc** của mọi automation framework chuyên nghiệp, đúng như JD mô tả *"phát triển, duy trì và thực thi kịch bản kiểm thử tự động"* — muốn "duy trì" được thì code phải có cấu trúc, không viết dồn hết vào 1 file test.

## 📘 Nội dung học
1. **Vấn đề khi không có POM**: locator lặp lại ở nhiều file test → 1 element đổi ID là phải sửa khắp nơi.
2. **Khái niệm POM**: mỗi trang web = 1 class (`LoginPage`, `CartPage`...), locator + hành động nằm trong class đó (dùng lại kiến thức OOP ở Bài 05), file test chỉ gọi method, không chứa locator.
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
4. **`BasePage`**: class cha chứa hành vi chung (vd `self.page = page`, method điều hướng), các page khác kế thừa từ đây (áp dụng kế thừa đã học ở Bài 05).
5. Refactor: chuyển code tuần 5-6 từ viết thẳng trong test sang cấu trúc POM.

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
