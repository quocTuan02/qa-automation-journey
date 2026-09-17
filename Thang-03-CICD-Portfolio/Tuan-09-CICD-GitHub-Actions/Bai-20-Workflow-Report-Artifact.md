# Bài 20: Viết workflow chạy Pytest tự động + upload report

**Tháng 3 – Tuần 9** | Thời lượng gợi ý: 2 ngày + 1 ngày xử lý lỗi pipeline

## 🎯 Mục tiêu
- Có 1 pipeline CI/CD thật sự chạy được: mỗi lần push code, GitHub tự động cài môi trường, chạy toàn bộ test, và lưu lại report.

## 📘 Nội dung học
1. **Action có sẵn**: `actions/checkout` (lấy code từ repo về máy ảo runner — không có bước này thì runner không có gì để chạy vì nó khởi động trống trơn), `actions/setup-python` (cài đúng phiên bản Python bạn khai báo, vì runner của GitHub không có sẵn version bạn cần).

   ```yaml
   steps:
     - uses: actions/checkout@v4
     - uses: actions/setup-python@v5
       with:
         python-version: "3.11"
   ```

2. **Cài dependencies trong workflow**: giống hệt việc cài `venv` trên máy cá nhân ở Bài 08, nhưng chạy trên máy ảo của GitHub mỗi lần workflow khởi động (máy ảo này "sạch" hoàn toàn, không có gì cài sẵn).

   ```yaml
     - name: Install dependencies
       run: |
         pip install -r requirements.txt
         playwright install --with-deps
   ```

3. **Chạy test trong workflow**: chỉ đơn giản là gọi đúng lệnh `pytest` bạn vẫn chạy ở máy cá nhân, kèm cờ xuất report.

   ```yaml
     - name: Run tests
       run: pytest --html=report.html --self-contained-html
   ```

4. **Upload artifact**: máy ảo runner sẽ bị GitHub xóa sạch ngay sau khi workflow chạy xong, nên nếu không "upload" file report ra ngoài thì report cũng biến mất theo. `actions/upload-artifact` đóng gói file/folder chỉ định và lưu lại trên GitHub để tải về xem sau.

   ```yaml
     - name: Upload report
       if: always()                     # upload cả khi test fail, không chỉ khi pass
       uses: actions/upload-artifact@v4
       with:
         name: pytest-report
         path: report.html
   ```

5. **Đọc log lỗi khi pipeline fail**: vào tab **Actions** trên GitHub → chọn đúng lần chạy bị đỏ (❌) → mở rộng từng step để xem log chi tiết. Lỗi hay gặp nhất ở người mới: quên chạy `playwright install --with-deps` (báo lỗi "Executable doesn't exist") hoặc quên set secret cho biến môi trường (test báo `KeyError`/`None`).

   *Ví dụ log lỗi điển hình:*
   ```text
   Error: browserType.launch: Executable doesn't exist at
   /home/runner/.cache/ms-playwright/chromium-.../chrome
   ```
   → nguyên nhân: thiếu bước `playwright install --with-deps` trong workflow.

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
