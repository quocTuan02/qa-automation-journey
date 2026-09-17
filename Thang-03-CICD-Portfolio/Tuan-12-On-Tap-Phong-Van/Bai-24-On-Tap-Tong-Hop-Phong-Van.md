# Bài 24: Ôn tập tổng hợp + Luyện phỏng vấn

**Tháng 3 – Tuần 12** | Thời lượng gợi ý: cả tuần

## 🎯 Mục tiêu
- Chuẩn hóa lại kiến thức 3 tháng thành câu trả lời mạch lạc, tự tin đối chiếu từng dòng JD với những gì bạn đã làm được.

## 📘 Nội dung học (ôn tập, đối chiếu JD)
1. **Test fundamentals** (JD: *"kiến thức vững chắc về phương pháp kiểm thử, cấp độ kiểm thử, vòng đời lỗi..."*):
   - Test pyramid, test level (unit/integration/system/acceptance), test type (functional/regression/smoke/exploratory).
   - Defect lifecycle: New → Assigned → Open → Fixed → Retest → Closed/Reopened.
   - Cách viết test case/test script/test data tốt (ôn lại Bài 23).
2. **Automation & POM**: chuẩn bị giải thích được "vì sao dùng POM", "flaky test là gì và xử lý thế nào" (retry, wait đúng cách, tránh test phụ thuộc lẫn nhau).
3. **API testing**: phân biệt test API bằng Postman (thủ công) vs tự động hóa; REST cơ bản.
4. **CI/CD**: giải thích được pipeline của chính project bạn làm hoạt động ra sao, từ push code tới khi có report.
5. **JMeter/OWASP/Selenium**: ôn lại khái niệm chính đã học Tuần 10, đủ để trả lời ở mức "hiểu và có thể học nhanh khi công ty cần".
6. **Soft skill theo JD**: cách trình bày rủi ro/tiến độ cho stakeholder, cách tham gia peer review — chuẩn bị 1-2 ví dụ tình huống cụ thể (dùng chính kinh nghiệm test thủ công trước đây của bạn để kể chuyện thật).

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
