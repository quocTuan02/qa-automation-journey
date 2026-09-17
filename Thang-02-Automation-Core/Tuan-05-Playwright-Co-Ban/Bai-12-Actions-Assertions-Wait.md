# Bài 12: Actions, Assertions, Wait strategies

**Tháng 2 – Tuần 5** | Thời lượng gợi ý: 2 ngày + 1 ngày bài tập tổng hợp

## 🎯 Mục tiêu
- Thực hiện được hành động trên trang web và **khẳng định (assert)** kết quả đúng như mong đợi — đây chính là bản chất của 1 test tự động.

## 📘 Nội dung học
1. **Actions**: là các hành động mô phỏng thao tác của người dùng thật lên phần tử đã tìm được bằng locator (Bài 11). Mỗi action tương ứng 1 hành vi cụ thể: gõ chữ, click chuột, tick checkbox, chọn dropdown...

   ```python
   page.get_by_placeholder("Username").fill("standard_user")   # gõ chữ vào ô input
   page.get_by_placeholder("Password").fill("secret_sauce")
   page.get_by_text("Login").click()                            # click nút
   page.locator("#add-to-cart-sauce-labs-backpack").click()      # click nút thêm giỏ hàng
   page.locator("select[data-test='product_sort_container']").select_option("lohi")  # chọn dropdown
   page.get_by_role("checkbox").check()                          # tick checkbox
   ```

2. **Assertions của Playwright (`expect`)**: dùng để "khẳng định" trạng thái thực tế trên trang đúng như mong đợi — đây chính là bước quyết định test PASS hay FAIL. Khác với `assert` thường của Python (kiểm tra ngay lập tức, giá trị đã cố định), `expect()` của Playwright tự động **retry** trong vài giây — rất hợp với web vì phần tử có thể xuất hiện chậm 1 chút do gọi API/render.

   ```python
   from playwright.sync_api import expect

   page.get_by_text("Login").click()
   expect(page.locator(".title")).to_have_text("Products")      # đợi & so khớp text
   expect(page.locator(".shopping_cart_badge")).to_be_visible() # đợi phần tử hiện ra
   expect(page.get_by_placeholder("Username")).to_have_value("standard_user")
   ```

3. **Wait strategies**: Playwright tự "chờ" phần tử sẵn sàng (đã render, không bị che, có thể click được) trước khi thực hiện action — gọi là **auto-waiting**. Nhờ vậy hầu như không bao giờ cần `time.sleep()` (cách làm cũ, không đáng tin cậy vì chờ 1 khoảng thời gian cố định dù trang xong sớm hay muộn). Chỉ cần chờ thủ công trong vài tình huống đặc biệt (chờ 1 request mạng, chờ trang load xong hẳn):

   ```python
   page.wait_for_load_state("networkidle")   # chờ trang hết gọi API ngầm
   page.wait_for_selector(".loading-spinner", state="hidden")  # chờ spinner biến mất
   ```

4. **Chạy nhiều trình duyệt**: Playwright hỗ trợ chạy cùng 1 test trên Chromium, Firefox, WebKit (engine của Safari) mà không cần sửa code — hữu ích để phát hiện lỗi chỉ xảy ra trên 1 trình duyệt cụ thể. Chế độ **headless** (không hiện giao diện, chạy nhanh, dùng khi chạy hàng loạt/CI) khác **headed** (có giao diện, dùng khi debug bằng mắt).

   ```python
   browser = p.chromium.launch(headless=True)   # chạy ẩn, nhanh — dùng khi CI/CD
   browser = p.firefox.launch(headless=False)   # chạy có giao diện trên Firefox — dùng khi debug
   ```

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
