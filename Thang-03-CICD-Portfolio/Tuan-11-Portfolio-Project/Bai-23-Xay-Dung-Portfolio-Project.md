# Bài 23: Xây dựng Portfolio Project hoàn chỉnh

**Tháng 3 – Tuần 11** | Thời lượng gợi ý: cả tuần (5-7 ngày)

## 🎯 Mục tiêu
- Tổng hợp toàn bộ kiến thức 10 tuần qua thành **1 project automation framework hoàn chỉnh** — đây chính là bằng chứng cụ thể nhất khi phỏng vấn, thay thế cho "3 năm kinh nghiệm" mà bạn chưa có ở mảng automation.

## 📘 Nội dung học (áp dụng, không có kiến thức mới)
Project cần thể hiện đầy đủ những gì JD yêu cầu:
1. **Automation UI**: Playwright + Pytest, cấu trúc **Page Object Model** rõ ràng (`pages/`, `tests/`).
2. **Automation API**: dùng `requests` (hoặc Playwright `APIRequestContext`) test 1 API demo, có cả test case dữ liệu hợp lệ/không hợp lệ.
3. **Test data**: tách riêng test data ra file (`json`/`csv`) hoặc `parametrize`, không hard-code trong test.
4. **CI/CD**: GitHub Actions tự động chạy toàn bộ test khi push code.
5. **Report**: xuất được report (`pytest-html` hoặc Allure), lưu lại làm artifact trên CI.
6. **Tài liệu**: `README.md` mô tả rõ mục đích, công nghệ dùng, cách cài đặt và chạy test, ảnh chụp report.
7. **Mô phỏng bug tracking**: tạo 1 bug giả định (cố tình để 1 test fail có lý do rõ ràng), viết 1 "bug report" mẫu theo chuẩn JIRA (title, steps to reproduce, expected/actual result, severity) — dù không có JIRA thật, viết vào `BUG_REPORT_SAMPLE.md` để thể hiện kỹ năng ghi nhận lỗi JD yêu cầu.

## 📚 Tài liệu tham khảo
- [Ứng dụng để test](https://www.saucedemo.com) + [API demo](https://reqres.in) (đã dùng suốt lộ trình) — hoặc chọn 1 app/API khác nếu muốn thể hiện sự chủ động.
- [Awesome README templates](https://github.com/othneildrew/Best-README-Template) — tham khảo cách trình bày README chuyên nghiệp.
- Xem lại các bài: 15-16 (POM + Report), 17-18 (API), 19-20 (CI/CD) để ráp nối thành project hoàn chỉnh.

## ✍️ Bài tập (deliverable cả tuần)
1. Lên kế hoạch: viết ra tối thiểu 15-20 test case (UI + API) bạn định tự động hóa — giống 1 test plan thật sự trước khi code (đúng JD *"chuẩn bị... kế hoạch kiểm thử"*).
2. Code toàn bộ framework theo cấu trúc POM, đảm bảo chạy xanh 100% local.
3. Thiết lập CI/CD chạy tự động, upload report artifact.
4. Viết `README.md` đầy đủ + `BUG_REPORT_SAMPLE.md`.
5. Push toàn bộ lên GitHub, kiểm tra lại: người lạ clone repo về, làm theo README có chạy được test không (nhờ bạn bè thử nếu có thể).
