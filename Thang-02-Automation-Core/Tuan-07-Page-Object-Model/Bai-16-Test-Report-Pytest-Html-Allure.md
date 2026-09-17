# Bài 16: Test Report — pytest-html / Allure Report

**Tháng 2 – Tuần 7** | Thời lượng gợi ý: 2 ngày + 1 ngày review code

## 🎯 Mục tiêu
- Xuất báo cáo test rõ ràng — đúng yêu cầu JD *"chuẩn bị các báo cáo thực hiện kiểm thử rõ ràng và truyền đạt các rủi ro..."*. Report cũng là thứ bạn sẽ đính kèm vào portfolio project ở tháng 3.

## 📘 Nội dung học
1. **`pytest-html`**: cài `pip install pytest-html`, chạy `pytest --html=report.html --self-contained-html` để ra 1 file HTML report duy nhất.
2. **Allure Report** (nâng cao hơn, đẹp và chi tiết hơn): cài `allure-pytest`, cần cài thêm Allure command line tool; các annotation `@allure.step`, `@allure.title` để report rõ ràng theo từng bước.
3. **Chụp screenshot khi test fail**: cấu hình `pytest-playwright` tự động chụp ảnh/quay video khi test fail (`--screenshot=only-on-failure`, `--video=retain-on-failure`) — cực hữu ích khi debug và khi báo cáo lỗi.
4. **Review code & docstring**: dọn dẹp code tuần 5-7, thêm docstring ngắn cho mỗi Page class và method mô tả nó làm gì.

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
