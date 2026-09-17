# Bài 12: Actions, Assertions, Wait strategies

**Tháng 2 – Tuần 5** | Thời lượng gợi ý: 2 ngày + 1 ngày bài tập tổng hợp

## 🎯 Mục tiêu
- Thực hiện được hành động trên trang web và **khẳng định (assert)** kết quả đúng như mong đợi — đây chính là bản chất của 1 test tự động.

## 📘 Nội dung học
1. **Actions**: `.click()`, `.fill()`, `.check()/.uncheck()`, `.select_option()`, `.hover()`, `.press()`.
2. **Assertions của Playwright (`expect`)**: `expect(locator).to_be_visible()`, `.to_have_text()`, `.to_have_value()`, `.to_be_checked()` — khác gì với `assert` thường của Python (auto-retry).
3. **Wait strategies**: vì sao Playwright tự động chờ phần tử sẵn sàng (auto-waiting) — không cần `time.sleep()` như Selenium cũ; khi nào vẫn cần chờ thủ công (`page.wait_for_selector`, `page.wait_for_load_state`).
4. **Chạy nhiều trình duyệt**: chạy test trên Chromium/Firefox/WebKit, chế độ headless vs có giao diện.

## 📚 Tài liệu tham khảo
- [Playwright Docs – Actions](https://playwright.dev/python/docs/input)
- [Playwright Docs – Assertions](https://playwright.dev/python/docs/test-assertions) (lưu ý: một số API assertion viết cho Pytest-playwright, đọc kèm phần Python sync)
- [Playwright Docs – Auto-waiting](https://playwright.dev/python/docs/actionability)

## ✍️ Bài tập
1. Viết script tự động hóa toàn bộ luồng **login** trên saucedemo.com (đúng user/pass hợp lệ), assert sau khi login thành công thấy đúng tiêu đề trang "Products".
2. Viết thêm case login **sai mật khẩu**, assert hiển thị đúng thông báo lỗi.
3. Trên demoqa.com, luyện thao tác với dropdown (`select_option`), checkbox (`check`), radio button — mỗi thao tác đều có `expect()` xác nhận trạng thái đúng.
4. Thử chạy cùng 1 script ở chế độ `headless=False` và `headless=True`, so sánh tốc độ chạy.
5. **Bài tập tổng hợp tuần 5**: Tự động hóa luồng: mở saucedemo → login → thêm 1 sản phẩm vào giỏ hàng → vào giỏ hàng → assert sản phẩm xuất hiện đúng tên/giá.
