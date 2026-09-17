# Bài 19: CI/CD là gì? Cấu trúc file YAML

**Tháng 3 – Tuần 9** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Hiểu khái niệm CI/CD và biết đọc/viết YAML — nền tảng để tự động chạy test mỗi khi code được push, đúng JD *"chạy các bài kiểm tra tự động trong các công cụ CI/CD như GitHub Actions, Jenkins hoặc GitLab CI"*.

## 📘 Nội dung học
1. **CI (Continuous Integration)**: mỗi lần push code, hệ thống tự động build/chạy test để phát hiện lỗi sớm. Ý tưởng cốt lõi: thay vì để lỗi tích tụ tới cuối sprint mới phát hiện, mỗi commit đều được kiểm tra ngay — tester/dev biết trong vài phút là code vừa push có làm gãy test nào không.

   *Ví dụ:* bạn push code sửa `login_page.py`, GitHub Actions tự động chạy `pytest` trong ~2 phút. Nếu test `test_login.py` fail, bạn nhận được email/thông báo đỏ ngay, không phải đợi ai đó chạy tay rồi báo lại.

2. **CD (Continuous Delivery/Deployment)**: biết khái niệm tổng quan (không cần thực hành sâu ở phần deploy). Delivery = code luôn ở trạng thái sẵn sàng deploy (cần người bấm nút để deploy thật); Deployment = tự động deploy thẳng lên production sau khi test pass, không cần người can thiệp.

   *Ví dụ:* 1 team e-commerce merge code vào `main` → CD tự động deploy lên môi trường staging để QA kiểm tra thêm trước khi release.

3. **YAML cơ bản**: indent bằng space (không dùng tab), key-value, list — cú pháp dùng trong GitHub Actions workflow. YAML rất nhạy cảm với thụt lề (2 space là chuẩn phổ biến); sai 1 khoảng trắng là file lỗi cú pháp ngay.

   *Ví dụ cú pháp:*
   ```yaml
   name: CI Test          # key: value
   on: push                # trigger đơn giản
   jobs:                   # jobs là 1 dict
     test-job:             # tên job, thụt lề 2 space so với "jobs"
       runs-on: ubuntu-latest
       steps:              # steps là 1 list
         - name: Checkout code
           uses: actions/checkout@v4
         - name: Run tests
           run: pytest
   ```

4. **GitHub Actions**: khái niệm `workflow` (toàn bộ quy trình tự động, định nghĩa trong 1 file `.yml`), `job` (1 nhóm công việc chạy trên 1 runner), `step` (từng bước nhỏ trong job, chạy tuần tự), `runner` (máy ảo Linux/Windows/macOS mà GitHub cấp để chạy job), trigger (`on: push`, `on: pull_request` — sự kiện nào thì workflow tự chạy).

   *Ví dụ:* workflow "CI Test" (1) trigger khi có `push` vào branch `main`, (2) có 1 job tên `test` chạy trên `runs-on: ubuntu-latest`, (3) job đó có 2 step: "Checkout code" và "Run tests".

5. **Secrets**: cách lưu biến nhạy cảm (API key, mật khẩu) an toàn trong GitHub Actions thay vì hard-code thẳng vào file YAML (rất nguy hiểm vì file này public trên repo).

   *Ví dụ:* vào **Settings → Secrets and variables → Actions** của repo, thêm secret tên `TEST_PASSWORD`, sau đó dùng trong workflow:
   ```yaml
   - name: Run tests with secret
     env:
       TEST_PASSWORD: ${{ secrets.TEST_PASSWORD }}
     run: pytest
   ```

## 📚 Tài liệu tham khảo
- [GitHub Docs – Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)
- [GitHub Docs – Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [YAML.org – tham khảo cú pháp](https://yaml.org/) hoặc [Learn YAML in Y minutes](https://learnxinyminutes.com/docs/yaml/)

## ✍️ Bài tập
1. Đọc và giải thích lại bằng lời của bạn: sự khác nhau giữa CI và CD, tại sao automation test lại gắn liền với CI.
2. Viết tay (không cần chạy) 1 file YAML mô phỏng cấu trúc: 1 workflow tên "CI Test", trigger khi push vào nhánh `main`, có 1 job gồm 2 step ("Checkout code", "Run tests").
3. Đọc 1 file `.github/workflows/*.yml` mẫu bất kỳ từ 1 repo public trên GitHub (tìm từ khóa "pytest github actions example"), chỉ ra từng phần: trigger, job, step, runner tương ứng với phần nào trong bài học.
