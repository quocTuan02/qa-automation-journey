# Bài 11: Cài đặt Playwright + Locator

**Tháng 2 – Tuần 5** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Cài đặt và chạy được test Playwright đầu tiên. Đây là bài đầu tiên chạm trực tiếp vào yêu cầu cốt lõi của JD: *"kinh nghiệm làm việc với framework tự động hóa"*.

## 📘 Nội dung học
1. **Cài đặt**: `pip install pytest-playwright`, sau đó `playwright install` (tải trình duyệt Chromium/Firefox/WebKit).
2. **Script Playwright đầu tiên**: mở browser, vào 1 trang web, đóng browser (sync API).
3. **Locator — cách "chỉ tay" vào phần tử trên trang**:
   - `page.get_by_role()`, `page.get_by_text()`, `page.get_by_label()`, `page.get_by_placeholder()` (locator theo ngữ nghĩa — cách Playwright khuyến khích).
   - CSS selector: `page.locator("css=...")` hoặc `page.locator("#id")`, `page.locator(".class")`.
   - XPath cơ bản (biết đọc, vì nhiều hệ thống cũ vẫn cần).
4. **Playwright Inspector / Codegen**: dùng `playwright codegen <url>` để tự sinh code khi thao tác bằng tay — công cụ học locator cực nhanh.

## 📚 Tài liệu tham khảo
- [Playwright Docs – Python – Getting Started](https://playwright.dev/python/docs/intro)
- [Playwright Docs – Locators](https://playwright.dev/python/docs/locators)
- [Playwright Docs – Codegen](https://playwright.dev/python/docs/codegen)
- Trang demo để luyện tập: [saucedemo.com](https://www.saucedemo.com) (chuyên để luyện automation), [demoqa.com](https://demoqa.com) (nhiều loại element: form, table, dropdown...)

## ✍️ Bài tập
1. Cài đặt xong Playwright, chạy được script mở `saucedemo.com`, chụp screenshot (`page.screenshot(path="...")`), đóng browser.
2. Dùng `playwright codegen https://www.saucedemo.com` để thao tác đăng nhập bằng tay, quan sát code Playwright tự sinh ra — đọc hiểu từng dòng.
3. Tự viết lại (không copy từ codegen) script: mở saucedemo, tìm ô username bằng `get_by_placeholder`, ô password tương tự, nút login bằng `get_by_text` hoặc CSS.
4. Trên demoqa.com, thử dùng cả 3 cách locator (role/text, CSS, XPath) để trỏ tới cùng 1 phần tử — so sánh độ ổn định/dễ đọc của từng cách.
