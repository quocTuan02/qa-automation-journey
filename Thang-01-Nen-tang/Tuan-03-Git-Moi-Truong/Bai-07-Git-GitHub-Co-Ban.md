# Bài 07: Git & GitHub cơ bản

**Tháng 1 – Tuần 3** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Quản lý version code, làm việc nhóm qua Git — bắt buộc trong mọi công ty có automation testing (framework luôn sống trên 1 repo Git), và cũng là điều kiện để chạy CI/CD tháng 3.

## 📘 Nội dung học

1. **Git cơ bản**: Git là công cụ quản lý phiên bản — ghi lại "lịch sử" thay đổi của code theo từng mốc (gọi là commit), cho phép quay lại bất kỳ mốc nào nếu cần. `git init` khởi tạo 1 repo (kho chứa) Git trong thư mục hiện tại, `git status` xem file nào đã sửa/chưa được lưu, `git add` đưa file vào "khu vực chuẩn bị" (staging), `git commit -m "..."` chốt lại 1 mốc thay đổi kèm mô tả, `git log` xem lại lịch sử các mốc đã commit.

   ```bash
   git init
   git status                              # xem file nào đang thay đổi/chưa track
   git add test_login.py                   # dua file vao staging
   git commit -m "feat: them test login co ban"
   git log --oneline                       # xem lich su commit ngan gon
   ```

2. **Kết nối GitHub**: GitHub là nơi lưu trữ repo Git trên mây, giúp backup code và làm việc nhóm. Sau khi tạo tài khoản và tạo repo trống trên GitHub, `git remote add origin <url>` gắn repo local với repo trên GitHub, `git push` đẩy commit local lên GitHub, `git pull` kéo thay đổi mới nhất từ GitHub về, `git clone` tải toàn bộ 1 repo có sẵn về máy.

   ```bash
   git remote add origin https://github.com/<username>/qa-automation-journey.git
   git branch -M main
   git push -u origin main                 # day code len GitHub lan dau
   git pull origin main                    # keo ban moi nhat ve (khi lam nhom)
   ```

3. **Branch**: 1 branch là 1 "nhánh" phát triển độc lập, giúp thử nghiệm/sửa code mà không ảnh hưởng tới nhánh `main` đang chạy ổn định. `git merge` gộp thay đổi từ 1 branch vào branch khác; nếu 2 branch cùng sửa 1 dòng thì xảy ra **conflict**, Git sẽ đánh dấu đoạn xung đột để bạn tự chọn giữ phần nào.

   ```bash
   git checkout -b feature/them-test-cart   # tao va chuyen sang branch moi
   # ... sua code, commit ...
   git checkout main
   git merge feature/them-test-cart          # gop nhanh vao main
   ```
   *Ví dụ conflict cần tự xử lý:*
   ```text
   <<<<<<< HEAD
   BASE_URL = "https://www.saucedemo.com"
   =======
   BASE_URL = "https://staging.saucedemo.com"
   >>>>>>> feature/them-test-cart
   ```
   → bạn sửa file để chỉ giữ lại đúng 1 dòng mong muốn, xóa các dấu `<<<<<<<`/`=======`/`>>>>>>>`, rồi `git add` + `git commit` để hoàn tất merge.

4. **`.gitignore`**: file liệt kê những đường dẫn/file Git sẽ **bỏ qua**, không theo dõi và không đẩy lên GitHub — dùng cho file không nên chia sẻ hoặc không cần thiết (môi trường ảo, cache, report tạm thời).

   ```text
   # .gitignore cho project Python
   venv/
   __pycache__/
   *.pyc
   report.html
   .idea/
   ```

5. **Viết README.md**: file Markdown hiển thị ngay ở trang chủ repo trên GitHub, dùng để giới thiệu project cho người khác (và cả bạn sau này) — mô tả project làm gì, cách cài đặt, cách chạy.

   ```markdown
   # QA Automation Journey

   Repo luyện tập automation testing với Python + Playwright + Pytest.

   ## Cài đặt
   \`\`\`bash
   pip install -r requirements.txt
   \`\`\`

   ## Chạy test
   \`\`\`bash
   pytest -v
   \`\`\`
   ```

6. **Pull Request (PR)**: khi làm việc nhóm, thay vì merge thẳng vào `main`, bạn tạo 1 Pull Request để đề xuất gộp branch của mình — đồng nghiệp review code, góp ý, rồi mới bấm merge. Đây là bước "code review" bắt buộc ở hầu hết công ty, giúp bắt lỗi sớm và giữ chất lượng code chung.

   *Ví dụ quy trình:* push branch `feature/them-test-cart` lên GitHub → vào tab "Pull Requests" → "New Pull Request" → chọn merge vào `main` → đồng nghiệp comment góp ý trực tiếp trên từng dòng code → sửa theo góp ý → merge khi đã được duyệt (approve).

## 📚 Tài liệu tham khảo
- [GitHub Docs – Git and GitHub learning resources](https://docs.github.com/en/get-started/start-your-journey/hello-world)
- [Learn Git Branching](https://learngitbranching.js.org/?locale=vi) — tool trực quan luyện branch/merge/conflict (có tiếng Việt).
- [Atlassian – Git Tutorial](https://www.atlassian.com/git/tutorials) — giải thích rõ ràng theo chủ đề.
- [gitignore.io](https://www.toptal.com/developers/gitignore) — sinh file `.gitignore` theo Python.

## ✍️ Bài tập
1. Cài Git, tạo tài khoản GitHub, tạo repo tên `qa-automation-journey` (public hoặc private đều được).
2. Push toàn bộ bài tập tuần 1 và tuần 2 lên repo này, mỗi bài 1 commit riêng với message rõ ràng (vd `"feat: bai tap ham so nguyen to"`).
3. Tạo 1 branch mới `practice-branch`, sửa 1 file, commit, rồi merge ngược lại `main`. Thử tạo conflict có chủ đích (sửa cùng 1 dòng ở 2 branch) và tự xử lý resolve conflict.
4. Viết file `README.md` cho repo mô tả: mục đích repo, cấu trúc thư mục, cách chạy code.
5. Thêm file `.gitignore` phù hợp cho project Python.
