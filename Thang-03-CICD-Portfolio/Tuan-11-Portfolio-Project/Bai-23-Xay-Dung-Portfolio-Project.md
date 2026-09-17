# Bài 23: Xây dựng Portfolio Project hoàn chỉnh

**Tháng 3 – Tuần 11** | Thời lượng gợi ý: cả tuần (5-7 ngày)

## 🎯 Mục tiêu
- Tổng hợp toàn bộ kiến thức 10 tuần qua thành **1 project automation framework hoàn chỉnh** — đây chính là bằng chứng cụ thể nhất khi phỏng vấn, thay thế cho "3 năm kinh nghiệm" mà bạn chưa có ở mảng automation.

## 📘 Nội dung học (áp dụng, không có kiến thức mới)
Project cần thể hiện đầy đủ những gì JD yêu cầu — đây là lúc ráp nối lại toàn bộ 22 bài học trước thành 1 sản phẩm hoàn chỉnh, không học thêm lý thuyết mới mà tập trung vào chất lượng và tính hoàn thiện:

1. **Automation UI**: Playwright + Pytest, cấu trúc **Page Object Model** rõ ràng (`pages/`, `tests/`) — áp dụng lại Bài 15.

   *Ví dụ cấu trúc thư mục project hoàn chỉnh:*
   ```
   qa-portfolio-project/
   ├── pages/
   │   ├── base_page.py
   │   ├── login_page.py
   │   └── inventory_page.py
   ├── tests/
   │   ├── ui/
   │   │   ├── test_login.py
   │   │   └── test_cart.py
   │   └── api/
   │       └── test_users_api.py
   ├── test_data/
   │   └── users.json
   ├── .github/workflows/tests.yml
   ├── BUG_REPORT_SAMPLE.md
   ├── requirements.txt
   └── README.md
   ```

2. **Automation API**: dùng `requests` (hoặc Playwright `APIRequestContext`) test 1 API demo, có cả test case dữ liệu hợp lệ/không hợp lệ — áp dụng lại Bài 17-18.

   *Ví dụ 1 test case API cần có trong `tests/api/test_users_api.py`:*
   ```python
   def test_get_user_khong_ton_tai():
       response = requests.get("https://reqres.in/api/users/9999")
       assert response.status_code == 404   # test case du lieu khong hop le
   ```

3. **Test data**: tách riêng test data ra file (`json`/`csv`) hoặc `parametrize`, không hard-code trong test — dữ liệu tách rời giúp thêm/sửa case mà không đụng vào logic test.

   *Ví dụ `test_data/users.json`:*
   ```json
   [
     {"username": "standard_user", "password": "secret_sauce", "expected": "success"},
     {"username": "locked_out_user", "password": "secret_sauce", "expected": "locked_error"}
   ]
   ```

4. **CI/CD**: GitHub Actions tự động chạy toàn bộ test khi push code — áp dụng lại Bài 19-20, dùng đúng file `.github/workflows/tests.yml` đã viết.

5. **Report**: xuất được report (`pytest-html` hoặc Allure), lưu lại làm artifact trên CI — áp dụng lại Bài 16.

6. **Tài liệu**: `README.md` mô tả rõ mục đích, công nghệ dùng, cách cài đặt và chạy test, ảnh chụp report.

   *Ví dụ khung README tối thiểu cần có:*
   ```markdown
   # QA Portfolio Project

   ## Mục đích
   Automation framework demo cho luồng login + giỏ hàng (saucedemo.com) và API user (reqres.in).

   ## Công nghệ
   Python 3.11, Playwright, Pytest, GitHub Actions, pytest-html

   ## Cách chạy
   \`\`\`bash
   pip install -r requirements.txt
   playwright install
   pytest --html=report.html --self-contained-html
   \`\`\`

   ## Kết quả mẫu
   ![report](docs/report-screenshot.png)
   ```

7. **Mô phỏng bug tracking**: tạo 1 bug giả định (cố tình để 1 test fail có lý do rõ ràng), viết 1 "bug report" mẫu theo chuẩn JIRA — dù không có JIRA thật, viết vào `BUG_REPORT_SAMPLE.md` để thể hiện kỹ năng ghi nhận lỗi JD yêu cầu.

   *Ví dụ nội dung `BUG_REPORT_SAMPLE.md`:*

   | Trường | Nội dung |
   |---|---|
   | **Title** | Giỏ hàng vẫn hiển thị số lượng "1" sau khi đã xóa sản phẩm duy nhất |
   | **Severity** | Medium |
   | **Environment** | Chrome (Playwright), saucedemo.com |
   | **Steps to reproduce** | 1. Login `standard_user` → 2. Thêm "Sauce Labs Backpack" vào giỏ → 3. Vào giỏ hàng, bấm "Remove" |
   | **Expected result** | Badge số lượng giỏ hàng biến mất (không còn hiển thị số) |
   | **Actual result** | Badge vẫn hiển thị "1" dù giỏ hàng trống |
   | **Attachment** | Screenshot/video Playwright tự chụp khi test `test_remove_last_item` fail |

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
