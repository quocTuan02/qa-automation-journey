# Bài 24: Ôn tập tổng hợp + Luyện phỏng vấn

**Tháng 3 – Tuần 12** | Thời lượng gợi ý: cả tuần

## 🎯 Mục tiêu
- Chuẩn hóa lại kiến thức 3 tháng thành câu trả lời mạch lạc, tự tin đối chiếu từng dòng JD với những gì bạn đã làm được.

## 📘 Nội dung học (ôn tập, đối chiếu JD)
1. **Test fundamentals** (JD: *"kiến thức vững chắc về phương pháp kiểm thử, cấp độ kiểm thử, vòng đời lỗi..."*):
   - **Test pyramid**: mô hình gợi ý tỉ lệ số lượng test theo từng tầng — nhiều **unit test** (nhanh, rẻ) ở đáy, ít dần **integration test** ở giữa, rất ít **UI/E2E test** (chậm, đắt) ở đỉnh.
   - **Test level**: unit (test 1 hàm/module riêng lẻ) → integration (test nhiều module ghép lại) → system (test toàn hệ thống) → acceptance (test theo góc nhìn nghiệp vụ/khách hàng).
   - **Test type**: functional (đúng chức năng), regression (đảm bảo tính năng cũ không bị vỡ sau khi sửa code mới), smoke (test nhanh các luồng quan trọng nhất trước khi test sâu), exploratory (khám phá tự do không theo kịch bản có sẵn).
   - **Defect lifecycle**: New → Assigned → Open → Fixed → Retest → Closed/Reopened.

   *Ví dụ trả lời phỏng vấn mẫu:* "Trong project portfolio của em, test API (`test_users_api.py`) đóng vai trò như integration test — nhanh và ổn định hơn UI test; test Playwright (`test_login.py`, `test_cart.py`) là E2E test, chạy chậm hơn nên em chỉ giữ số lượng vừa đủ cho các luồng quan trọng nhất (login, thêm giỏ hàng), đúng tinh thần test pyramid."

2. **Automation & POM**: chuẩn bị giải thích được "vì sao dùng POM" và "flaky test là gì, xử lý thế nào". **Flaky test** là test khi chạy lúc PASS lúc FAIL dù code không đổi — nguyên nhân phổ biến: chờ (wait) không đúng cách, test phụ thuộc thứ tự chạy của test khác, dữ liệu test bị người khác/lần chạy trước sửa mất.

   *Ví dụ câu trả lời mẫu:* "Em từng gặp flaky test khi test `add_to_cart` thỉnh thoảng fail vì element chưa kịp render. Playwright có auto-wait nên ít gặp hơn Selenium, nhưng em vẫn thêm `expect().to_be_visible()` thay vì click ngay, và tách dữ liệu test theo từng test (không dùng chung 1 tài khoản test giữa nhiều test chạy song song) để tránh test này ảnh hưởng test kia."

3. **API testing**: phân biệt test API bằng Postman (thủ công, dùng khi cần khám phá/verify nhanh 1 endpoint mới) vs tự động hóa (dùng khi cần chạy lại nhiều lần, tích hợp CI/CD); REST cơ bản (method, status code, JSON).

   *Ví dụ trả lời mẫu:* "Em dùng Postman khi mới nhận 1 API chưa quen để khám phá response trước, sau đó mới viết lại thành test tự động bằng `requests` + Pytest để chạy lặp lại được trong CI/CD mỗi lần có code mới."

4. **CI/CD**: giải thích được pipeline của chính project bạn làm hoạt động ra sao.

   *Ví dụ trả lời mẫu (mô tả đúng luồng đã làm ở Bài 19-20):* "Mỗi lần em push code lên GitHub, GitHub Actions tự động: checkout code → cài Python + dependencies → cài trình duyệt Playwright → chạy `pytest` cho cả test API lẫn UI → xuất report HTML và upload làm artifact. Nếu có test fail, em vào tab Actions đọc log để biết ngay nguyên nhân mà không cần chạy lại thủ công trên máy mình."

5. **JMeter/OWASP/Selenium**: ôn lại khái niệm chính đã học Tuần 10, đủ để trả lời ở mức "hiểu và có thể học nhanh khi công ty cần" — không cần trả lời như chuyên gia, chỉ cần cho thấy đã có nền và biết áp dụng khi cần.

   *Ví dụ trả lời mẫu:* "Em chưa có kinh nghiệm dự án thực tế với JMeter nhưng đã tự làm 1 test plan cơ bản đo response time của API khi tăng dần user ảo. Về bảo mật, em biết OWASP Top 10 và có thói quen thử input bất thường (SQL Injection, XSS) khi test form. Về Selenium, em học Playwright là chính nhưng đã viết thử lại cùng 1 test bằng Selenium nên đọc hiểu code Selenium không khó khăn gì."

6. **Soft skill theo JD**: cách trình bày rủi ro/tiến độ cho stakeholder, cách tham gia peer review — chuẩn bị 1-2 ví dụ tình huống cụ thể (dùng chính kinh nghiệm test thủ công trước đây của bạn để kể chuyện thật).

   *Ví dụ trả lời mẫu:* "Khi còn test thủ công, em từng phát hiện 1 lỗi nghiêm trọng gần sát ngày release; thay vì chỉ báo trong group chat, em viết hẳn 1 bug report rõ ràng (steps to reproduce, mức độ ảnh hưởng) và trao đổi trực tiếp với PM để team quyết định có trì hoãn release hay không — đúng tinh thần JD yêu cầu 'truyền đạt rủi ro về chất lượng sản phẩm cho các bên liên quan'."

## 📚 Tài liệu tham khảo
- [Ministry of Testing – Interview questions cho QA](https://www.ministryoftesting.com/) (cộng đồng lớn, nhiều bài chia sẻ kinh nghiệm phỏng vấn)
- [Playwright Docs](https://playwright.dev/python/docs/intro) / [Pytest Docs](https://docs.pytest.org/) — đọc lại phần bạn chưa chắc.
- Xem lại `README.md` gốc của lộ trình này (mục "Sau 3 tháng, bạn sẽ đối chiếu được với JD như sau") để tự chấm điểm bản thân theo từng gạch đầu dòng JD.

## ✍️ Bài tập
1. Viết ra giấy/file: trả lời 10 câu hỏi phỏng vấn phổ biến, ví dụ:
   - "Sự khác biệt giữa kiểm thử thủ công và tự động là gì, khi nào nên/không nên tự động hóa?"
   - "Page Object Model là gì, lợi ích cụ thể trong project của bạn?"
   - "Flaky test là gì, bạn xử lý thế nào?"
   - "CI/CD hoạt động thế nào trong project bạn làm?"
   - "Bạn dùng SQL để làm gì trong quá trình test?"
2. Chuẩn bị demo trực tiếp Portfolio Project (Bài 23): chạy được test local + trỏ vào GitHub Actions cho thấy pipeline chạy thật, mở report cho thấy kết quả.
3. Tự đối chiếu lại toàn bộ JD (mục Yêu cầu + Nên có) với những gì đã học/làm được trong 3 tháng — đánh dấu phần nào tự tin, phần nào cần học thêm sau khi đi làm.
4. Chuẩn bị CV/portfolio: liệt kê project vừa làm, link GitHub, công nghệ sử dụng (Python, Playwright, Pytest, SQL, Git, GitHub Actions) ngay đầu CV phần kỹ năng automation.
