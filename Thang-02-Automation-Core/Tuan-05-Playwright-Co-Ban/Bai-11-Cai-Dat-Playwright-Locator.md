# Bài 11: Cài đặt Playwright + Locator

**Tháng 2 – Tuần 5** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Cài đặt và chạy được test Playwright đầu tiên. Đây là bài đầu tiên chạm trực tiếp vào yêu cầu cốt lõi của JD: *"kinh nghiệm làm việc với framework tự động hóa"*.

## 📘 Nội dung học
1. **Cài đặt**: `pip install pytest-playwright`, sau đó `playwright install` (tải trình duyệt Chromium/Firefox/WebKit). Đây là lần đầu bạn cài 1 "bộ công cụ automation" thật sự — khác với thư viện Python thuần túy, Playwright cần tải kèm trình duyệt riêng (không dùng Chrome cài sẵn trên máy) để đảm bảo test chạy ổn định, không phụ thuộc version trình duyệt của máy.

   ```bash
   pip install pytest-playwright
   playwright install
   ```

2. **Script Playwright đầu tiên**: quy trình chuẩn của mọi script Playwright là mở trình duyệt → mở 1 tab (page) → vào URL → thao tác → đóng trình duyệt. Ở giai đoạn này ta viết bằng "sync API" thuần (chưa dùng Pytest) để hiểu rõ vòng đời trước khi giao việc mở/đóng browser cho fixture của Pytest ở Bài 13.

   ```python
   from playwright.sync_api import sync_playwright

   with sync_playwright() as p:
       browser = p.chromium.launch(headless=False)   # mở Chromium, có giao diện
       page = browser.new_page()                     # mở 1 tab mới
       page.goto("https://www.saucedemo.com")         # vào trang
       print(page.title())                            # in tiêu đề trang ra console
       browser.close()                                # luôn đóng browser khi xong
   ```

3. **Locator — cách "chỉ tay" vào phần tử trên trang**: locator là bước quan trọng nhất của UI automation — phải trỏ đúng và ổn định vào 1 phần tử (nút, ô nhập liệu...) thì mới thao tác được. Playwright cho 3 cách, ưu tiên theo thứ tự sau:
   - **Locator theo ngữ nghĩa (khuyến khích nhất)**: mô tả phần tử theo cách người dùng nhìn thấy (vai trò, chữ hiển thị, placeholder) thay vì phụ thuộc vào cấu trúc HTML — nên ít bị vỡ khi dev đổi code.
     ```python
     page.get_by_placeholder("Username").fill("standard_user")
     page.get_by_role("button", name="Login").click()
     page.get_by_text("Products").is_visible()
     ```
   - **CSS selector**: dùng khi phần tử không có role/text rõ ràng, dựa vào `id`/`class`/attribute trong HTML.
     ```python
     page.locator("#user-name").fill("standard_user")   # theo id
     page.locator(".btn_action").click()                # theo class
     ```
   - **XPath**: ít dùng hơn với Playwright hiện đại, nhưng vẫn cần biết đọc vì nhiều hệ thống/tài liệu cũ dùng.
     ```python
     page.locator("xpath=//button[@id='login-button']").click()
     ```

4. **Playwright Inspector / Codegen**: thay vì đoán locator bằng mắt, dùng lệnh `playwright codegen <url>` để mở 1 trình duyệt có ghi lại thao tác — bạn click/gõ như người dùng thật, Playwright tự sinh ra code Python tương ứng kèm locator được chọn tự động theo best-practice. Đây là cách học locator nhanh nhất khi mới bắt đầu.

   ```bash
   playwright codegen https://www.saucedemo.com
   ```
   Sau khi chạy lệnh trên, thử đăng nhập bằng tay trong cửa sổ hiện ra — quan sát code Python được sinh ra ở cửa sổ Inspector đi kèm.

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
