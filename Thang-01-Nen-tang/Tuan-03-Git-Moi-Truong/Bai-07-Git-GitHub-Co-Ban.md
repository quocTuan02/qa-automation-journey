# Bài 07: Git & GitHub cơ bản

**Tháng 1 – Tuần 3** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Quản lý version code, làm việc nhóm qua Git — bắt buộc trong mọi công ty có automation testing (framework luôn sống trên 1 repo Git), và cũng là điều kiện để chạy CI/CD tháng 3.

## 📘 Nội dung học
1. **Git cơ bản**: `git init`, `git status`, `git add`, `git commit -m "..."`, `git log`.
2. **Kết nối GitHub**: tạo tài khoản, tạo repo, `git remote add origin`, `git push`, `git pull`, `git clone`.
3. **Branch**: `git branch`, `git checkout -b`, `git merge`, xử lý conflict cơ bản khi merge.
4. **`.gitignore`**: loại trừ file không cần thiết (vd `venv/`, `__pycache__/`, file report).
5. **Thực hành viết README.md** mô tả project — kỹ năng cần cho portfolio project ở tháng 3.
6. (Biết sơ qua) **Pull Request**: khái niệm, vì sao dùng trong làm việc nhóm, code review.

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
