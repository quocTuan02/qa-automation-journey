# Bài 20: Viết workflow chạy Pytest tự động + upload report

**Tháng 3 – Tuần 9** | Thời lượng gợi ý: 2 ngày + 1 ngày xử lý lỗi pipeline

## 🎯 Mục tiêu
- Có 1 pipeline CI/CD thật sự chạy được: mỗi lần push code, GitHub tự động cài môi trường, chạy toàn bộ test, và lưu lại report.

## 📘 Nội dung học
1. **Action có sẵn**: `actions/checkout` (lấy code về), `actions/setup-python` (cài Python).
2. **Cài dependencies trong workflow**: `pip install -r requirements.txt`, `playwright install --with-deps`.
3. **Chạy test trong workflow**: step `run: pytest --html=report.html --self-contained-html`.
4. **Upload artifact**: dùng `actions/upload-artifact` để lưu lại file report, xem được report sau khi workflow chạy xong (dù chạy trên máy ảo GitHub, không phải máy mình).
5. **Đọc log lỗi khi pipeline fail**: cách debug khi workflow đỏ (failed) — thường do thiếu cài đặt trình duyệt hoặc thiếu biến môi trường.

## 📚 Tài liệu tham khảo
- [GitHub Docs – Building and testing Python](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python)
- [GitHub Marketplace – actions/upload-artifact](https://github.com/actions/upload-artifact)
- [Playwright Docs – Setting up CI](https://playwright.dev/python/docs/ci)

## ✍️ Bài tập
1. Tạo file `.github/workflows/tests.yml` trong repo, viết workflow: trigger khi push vào `main`, checkout code, setup Python, cài `requirements.txt`, cài Playwright browser.
2. Thêm step chạy `pytest` toàn bộ bộ test API (nhẹ hơn UI, dễ chạy thành công lần đầu trên CI).
3. Thêm step chạy bộ test UI Playwright (`--headed` không dùng được trên CI, phải chạy headless).
4. Thêm `actions/upload-artifact` để lưu `report.html`, push code, vào tab "Actions" trên GitHub xem workflow chạy, tải report về xem.
5. Cố tình làm 1 test fail, quan sát workflow báo đỏ, đọc log để xác định nguyên nhân, sửa và push lại tới khi pipeline chạy xanh hoàn toàn.
