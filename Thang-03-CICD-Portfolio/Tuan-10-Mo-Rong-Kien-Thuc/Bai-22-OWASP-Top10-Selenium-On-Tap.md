# Bài 22: OWASP Top 10 (kiến thức bảo mật cơ bản) + Ôn tập Selenium

**Tháng 3 – Tuần 10** | Thời lượng gợi ý: 2 ngày + 1 ngày ôn tập

## 🎯 Mục tiêu
- Đáp ứng phần "Nên có" của JD: *"kiến thức cơ bản về các khái niệm kiểm thử bảo mật và các rủi ro thường gặp đối với ứng dụng web"*.
- Biết đọc hiểu Selenium cơ bản để không bỡ ngỡ nếu công ty dùng framework này thay vì Playwright (JD liệt kê Selenium đầu tiên trong danh sách).

## 📘 Nội dung học
1. **OWASP Top 10** (bản mới nhất): đọc hiểu khái niệm, không cần thực hành khai thác — chỉ cần biết rủi ro là gì và vì sao tester cần quan tâm. Đây là danh sách 10 loại lỗ hổng bảo mật phổ biến/nguy hiểm nhất trên ứng dụng web, do cộng đồng OWASP tổng hợp và cập nhật định kỳ:
   - **SQL Injection**: kẻ tấn công chèn câu lệnh SQL vào ô input để thao túng câu truy vấn thật của hệ thống. Liên hệ trực tiếp tới kiến thức SQL bạn học ở Tuần 4: nếu backend nối chuỗi SQL trực tiếp từ input người dùng (`"SELECT * FROM users WHERE username='" + input + "'"`), kẻ tấn công có thể nhập `' OR '1'='1` để bypass điều kiện đăng nhập.
   - **Cross-Site Scripting (XSS)**: chèn đoạn script (thường là JavaScript) vào input, nếu ứng dụng hiển thị lại input đó ra trang mà không lọc, script sẽ tự chạy trên trình duyệt người khác xem trang.
   - **Broken Authentication**: lỗ hổng trong cơ chế đăng nhập/quản lý phiên (session) — vd không giới hạn số lần đăng nhập sai, để lộ token trong URL.
   - **Sensitive Data Exposure**: dữ liệu nhạy cảm (mật khẩu, số thẻ) không được mã hóa khi lưu trữ/truyền đi.
   - **Security Misconfiguration**: cấu hình hệ thống sai/thiếu an toàn (vd để lộ trang debug, mật khẩu mặc định chưa đổi).

   *Ví dụ liên hệ với công việc tester:* khi test tính năng "tìm kiếm sản phẩm", ngoài case functional bình thường, 1 tester có ý thức bảo mật sẽ thêm case: "nhập ký tự đặc biệt/script vào ô search, kiểm tra hệ thống không bị lỗi/không hiển thị script chạy được".

2. **Tư duy test bảo mật cơ bản cho tester (không phải pentester)**: thử input bất thường vào form để kiểm tra ứng dụng xử lý input có an toàn tối thiểu không — đây là **input validation testing**, nằm trong phạm vi functional/security-aware testing của QA (khác hoàn toàn với pentest chuyên sâu, việc đó thuộc đội security).

   *Ví dụ input cụ thể để thử (chỉ quan sát, không khai thác thật):*
   ```text
   Input test SQL Injection:   ' OR '1'='1
   Input test SQL Injection:   admin'--
   Input test XSS:             <script>alert('xss')</script>
   Input test XSS:             <img src=x onerror=alert(1)>
   ```
   *Kết quả mong đợi (ứng dụng an toàn):* form báo lỗi "sai định dạng"/không cho submit, hoặc hiển thị input đó ra màn hình dưới dạng text thuần (không chạy script, không có ảnh vỡ kèm alert) — nếu popup `alert()` thật sự bật lên nghĩa là ứng dụng có lỗ hổng XSS.

3. **Ôn tập Selenium**: Selenium là framework automation ra đời trước Playwright rất lâu, ý tưởng cốt lõi giống nhau (mở browser → tìm phần tử → thao tác → assert) nhưng cú pháp và cách chờ (wait) khác biệt: Selenium **không** tự động chờ phần tử sẵn sàng như Playwright, tester phải tự thêm `WebDriverWait` để tránh lỗi "element not found" do phần tử chưa kịp render.

   *Ví dụ Selenium — cùng 1 việc (login trên saucedemo) so với Playwright ở Bài 11-12:*
   ```python
   from selenium import webdriver
   from selenium.webdriver.common.by import By
   from selenium.webdriver.support.ui import WebDriverWait
   from selenium.webdriver.support import expected_conditions as EC

   driver = webdriver.Chrome()
   driver.get("https://www.saucedemo.com")

   # Selenium không tự chờ -> phải chủ động wait trước khi thao tác
   wait = WebDriverWait(driver, 10)
   username_box = wait.until(EC.presence_of_element_located((By.ID, "user-name")))
   username_box.send_keys("standard_user")

   driver.find_element(By.ID, "password").send_keys("secret_sauce")
   driver.find_element(By.ID, "login-button").click()

   assert "inventory" in driver.current_url
   driver.quit()   # phải tự đóng driver, Selenium không tự dọn dẹp như fixture "page" của pytest-playwright
   ```
   So với đoạn Playwright tương ứng ở Bài 12 (`page.get_by_placeholder(...).fill(...)` + `expect(...)` tự retry), có thể thấy Selenium cần nhiều dòng chờ thủ công hơn và phải tự quản lý vòng đời driver.

## 📚 Tài liệu tham khảo
- [OWASP Top 10 – trang chính thức](https://owasp.org/www-project-top-ten/)
- [OWASP – Testing Guide (tổng quan)](https://owasp.org/www-project-web-security-testing-guide/)
- [Selenium Docs – Getting Started (Python)](https://www.selenium.dev/documentation/webdriver/getting_started/)

## ✍️ Bài tập
1. Đọc OWASP Top 10, tóm tắt lại bằng lời của bạn 5 rủi ro mà bạn thấy liên quan trực tiếp nhất tới công việc test (vd SQL Injection dễ liên hệ với phần SQL đã học).
2. Thử nhập input `<script>alert('test')</script>` và `' OR '1'='1` vào 1 form bất kỳ trên demoqa.com, quan sát và ghi nhận ứng dụng xử lý input đó như thế nào (không tấn công thật, chỉ quan sát input validation).
3. Cài `selenium` + `webdriver-manager`, viết lại 1 test login đơn giản trên saucedemo bằng Selenium (tương tự bài đã làm với Playwright ở Tuần 5) để so sánh trực tiếp cú pháp 2 framework.
4. Viết bảng so sánh ngắn (Selenium vs Playwright): auto-wait, cú pháp locator, tốc độ, hỗ trợ ngôn ngữ — để tự tin trả lời nếu phỏng vấn hỏi "bạn có biết Selenium không".
