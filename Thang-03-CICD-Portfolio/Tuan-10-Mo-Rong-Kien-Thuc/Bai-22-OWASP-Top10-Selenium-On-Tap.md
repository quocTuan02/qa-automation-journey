# Bài 22: OWASP Top 10 (kiến thức bảo mật cơ bản) + Ôn tập Selenium

**Tháng 3 – Tuần 10** | Thời lượng gợi ý: 2 ngày + 1 ngày ôn tập

## 🎯 Mục tiêu
- Đáp ứng phần "Nên có" của JD: *"kiến thức cơ bản về các khái niệm kiểm thử bảo mật và các rủi ro thường gặp đối với ứng dụng web"*.
- Biết đọc hiểu Selenium cơ bản để không bỡ ngỡ nếu công ty dùng framework này thay vì Playwright (JD liệt kê Selenium đầu tiên trong danh sách).

## 📘 Nội dung học
1. **OWASP Top 10** (bản mới nhất): đọc hiểu khái niệm, không cần thực hành khai thác — chỉ cần biết rủi ro là gì và vì sao tester cần quan tâm:
   - SQL Injection, Cross-Site Scripting (XSS), Broken Authentication, Sensitive Data Exposure, Security Misconfiguration...
2. **Tư duy test bảo mật cơ bản cho tester (không phải pentester)**: thử input bất thường vào form (`' OR '1'='1`, `<script>alert(1)</script>`) để kiểm tra ứng dụng xử lý input có an toàn tối thiểu không — đây là input validation testing, nằm trong phạm vi functional/security-aware testing của QA.
3. **Ôn tập Selenium**: cấu trúc cơ bản (`webdriver.Chrome()`, `driver.find_element(By.ID, "...")`, `driver.get()`), so sánh nhanh với Playwright (API tương tự về ý tưởng, khác cú pháp và cách auto-wait).

## 📚 Tài liệu tham khảo
- [OWASP Top 10 – trang chính thức](https://owasp.org/www-project-top-ten/)
- [OWASP – Testing Guide (tổng quan)](https://owasp.org/www-project-web-security-testing-guide/)
- [Selenium Docs – Getting Started (Python)](https://www.selenium.dev/documentation/webdriver/getting_started/)

## ✍️ Bài tập
1. Đọc OWASP Top 10, tóm tắt lại bằng lời của bạn 5 rủi ro mà bạn thấy liên quan trực tiếp nhất tới công việc test (vd SQL Injection dễ liên hệ với phần SQL đã học).
2. Thử nhập input `<script>alert('test')</script>` và `' OR '1'='1` vào 1 form bất kỳ trên demoqa.com, quan sát và ghi nhận ứng dụng xử lý input đó như thế nào (không tấn công thật, chỉ quan sát input validation).
3. Cài `selenium` + `webdriver-manager`, viết lại 1 test login đơn giản trên saucedemo bằng Selenium (tương tự bài đã làm với Playwright ở Tuần 5) để so sánh trực tiếp cú pháp 2 framework.
4. Viết bảng so sánh ngắn (Selenium vs Playwright): auto-wait, cú pháp locator, tốc độ, hỗ trợ ngôn ngữ — để tự tin trả lời nếu phỏng vấn hỏi "bạn có biết Selenium không".
