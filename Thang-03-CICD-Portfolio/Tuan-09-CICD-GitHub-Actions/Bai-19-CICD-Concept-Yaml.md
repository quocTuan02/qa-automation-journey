# Bài 19: CI/CD là gì? Cấu trúc file YAML

**Tháng 3 – Tuần 9** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Hiểu khái niệm CI/CD và biết đọc/viết YAML — nền tảng để tự động chạy test mỗi khi code được push, đúng JD *"chạy các bài kiểm tra tự động trong các công cụ CI/CD như GitHub Actions, Jenkins hoặc GitLab CI"*.

## 📘 Nội dung học
1. **CI (Continuous Integration)**: mỗi lần push code, hệ thống tự động build/chạy test để phát hiện lỗi sớm.
2. **CD (Continuous Delivery/Deployment)**: biết khái niệm tổng quan (không cần thực hành sâu ở phần deploy).
3. **YAML cơ bản**: indent bằng space (không dùng tab), key-value, list — cú pháp dùng trong GitHub Actions workflow.
4. **GitHub Actions**: khái niệm `workflow`, `job`, `step`, `runner` (máy ảo chạy job), trigger (`on: push`, `on: pull_request`).
5. **Secrets**: cách lưu biến nhạy cảm (API key, mật khẩu) an toàn trong GitHub Actions thay vì hard-code.

## 📚 Tài liệu tham khảo
- [GitHub Docs – Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)
- [GitHub Docs – Workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [YAML.org – tham khảo cú pháp](https://yaml.org/) hoặc [Learn YAML in Y minutes](https://learnxinyminutes.com/docs/yaml/)

## ✍️ Bài tập
1. Đọc và giải thích lại bằng lời của bạn: sự khác nhau giữa CI và CD, tại sao automation test lại gắn liền với CI.
2. Viết tay (không cần chạy) 1 file YAML mô phỏng cấu trúc: 1 workflow tên "CI Test", trigger khi push vào nhánh `main`, có 1 job gồm 2 step ("Checkout code", "Run tests").
3. Đọc 1 file `.github/workflows/*.yml` mẫu bất kỳ từ 1 repo public trên GitHub (tìm từ khóa "pytest github actions example"), chỉ ra từng phần: trigger, job, step, runner tương ứng với phần nào trong bài học.
