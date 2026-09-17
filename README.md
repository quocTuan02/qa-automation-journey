# Lộ trình 3 tháng: Manual Tester → QA Automation Engineer

Lộ trình này được thiết kế riêng cho người đã có nền tảng **test thủ công** và **SQL cơ bản**, lâu chưa code, nhắm tới vị trí **QA Automation Engineer** với JD yêu cầu:

- 3+ năm kinh nghiệm kiểm thử, có automation
- Vững kiến thức test method, test level, defect lifecycle
- Viết được test script/test case/test data/test description
- Biết ít nhất 1 framework automation (chọn: **Python + Playwright + Pytest**)
- Kiểm thử API (Postman + tự động hóa)
- SQL cơ bản để chuẩn bị/kiểm tra test data
- Nên có: JMeter/Locust (performance), kiến thức bảo mật cơ bản, CI/CD (GitHub Actions/Jenkins/GitLab CI)

> Stack chính được chọn: **Python + Playwright + Pytest** (dễ học lại với người lâu không code, mạnh cả UI lẫn API, đang là xu hướng). Tuần 22 có ôn tập nhanh Selenium để không bỡ ngỡ nếu công ty dùng framework khác.

## Cách dùng repo này

- Mỗi **Tuần** là 1 folder lớn, chứa các **Bài học** (file `.md`) học trong tuần đó.
- Mỗi bài học có 3 phần cố định: **Nội dung học** → **Tài liệu tham khảo** → **Bài tập**.
- Học xong bài nào, làm bài tập ngay bài đó, code thực hành nên đẩy lên 1 repo GitHub riêng (tạo ở Tuần 3) để vừa luyện Git vừa có bằng chứng cho CV/phỏng vấn.

## Lịch tổng quan

### Tháng 1 — Nền tảng (`Thang-01-Nen-tang/`)
| Tuần | Chủ đề | Bài học |
|---|---|---|
| 1 | Python cơ bản | [Bài 01: Biến, kiểu dữ liệu, toán tử](Thang-01-Nen-tang/Tuan-01-Python-Co-Ban/Bai-01-Cai-Dat-Bien-Kieu-Du-Lieu-Toan-Tu.md)<br>[Bài 02: Điều kiện & vòng lặp](Thang-01-Nen-tang/Tuan-01-Python-Co-Ban/Bai-02-Dieu-Kien-Vong-Lap.md)<br>[Bài 03: Hàm (function)](Thang-01-Nen-tang/Tuan-01-Python-Co-Ban/Bai-03-Ham-Function.md) |
| 2 | Python trung cấp + OOP | [Bài 04: List/Dict/String nâng cao](Thang-01-Nen-tang/Tuan-02-Python-OOP/Bai-04-List-Dict-String-Nang-Cao.md)<br>[Bài 05: OOP — Class/Object](Thang-01-Nen-tang/Tuan-02-Python-OOP/Bai-05-OOP-Class-Object.md)<br>[Bài 06: Exception & File I/O](Thang-01-Nen-tang/Tuan-02-Python-OOP/Bai-06-Exception-File-IO.md) |
| 3 | Git & môi trường làm việc | [Bài 07: Git & GitHub cơ bản](Thang-01-Nen-tang/Tuan-03-Git-Moi-Truong/Bai-07-Git-GitHub-Co-Ban.md)<br>[Bài 08: VSCode/venv/pip](Thang-01-Nen-tang/Tuan-03-Git-Moi-Truong/Bai-08-VSCode-Venv-Pip.md) |
| 4 | SQL nâng cao cho tester | [Bài 09: JOIN/GROUP BY/HAVING](Thang-01-Nen-tang/Tuan-04-SQL-Nang-Cao/Bai-09-Join-Group-By-Having.md)<br>[Bài 10: Subquery/Aggregate/CASE WHEN](Thang-01-Nen-tang/Tuan-04-SQL-Nang-Cao/Bai-10-Subquery-Aggregate-Case-When.md) |

### Tháng 2 — Automation Core (`Thang-02-Automation-Core/`)
| Tuần | Chủ đề | Bài học |
|---|---|---|
| 5 | Playwright cơ bản | [Bài 11: Cài đặt Playwright + Locator](Thang-02-Automation-Core/Tuan-05-Playwright-Co-Ban/Bai-11-Cai-Dat-Playwright-Locator.md)<br>[Bài 12: Actions/Assertions/Wait](Thang-02-Automation-Core/Tuan-05-Playwright-Co-Ban/Bai-12-Actions-Assertions-Wait.md) |
| 6 | Pytest + Playwright | [Bài 13: Cấu trúc Pytest/Fixture](Thang-02-Automation-Core/Tuan-06-Pytest-Playwright/Bai-13-Cau-Truc-Pytest-Fixture.md)<br>[Bài 14: Parametrize/Setup-Teardown](Thang-02-Automation-Core/Tuan-06-Pytest-Playwright/Bai-14-Parametrize-Setup-Teardown.md) |
| 7 | Page Object Model | [Bài 15: Khái niệm POM + refactor](Thang-02-Automation-Core/Tuan-07-Page-Object-Model/Bai-15-POM-Concept-Refactor.md)<br>[Bài 16: Test report (pytest-html/Allure)](Thang-02-Automation-Core/Tuan-07-Page-Object-Model/Bai-16-Test-Report-Pytest-Html-Allure.md) |
| 8 | API Testing cơ bản | [Bài 17: Postman/Swagger](Thang-02-Automation-Core/Tuan-08-API-Testing-Co-Ban/Bai-17-Postman-Swagger.md)<br>[Bài 18: Requests library + Pytest](Thang-02-Automation-Core/Tuan-08-API-Testing-Co-Ban/Bai-18-Requests-Library-Pytest.md) |

### Tháng 3 — CI/CD & Portfolio (`Thang-03-CICD-Portfolio/`)
| Tuần | Chủ đề | Bài học |
|---|---|---|
| 9 | CI/CD với GitHub Actions | [Bài 19: Khái niệm CI/CD + YAML](Thang-03-CICD-Portfolio/Tuan-09-CICD-GitHub-Actions/Bai-19-CICD-Concept-Yaml.md)<br>[Bài 20: Workflow + report artifact](Thang-03-CICD-Portfolio/Tuan-09-CICD-GitHub-Actions/Bai-20-Workflow-Report-Artifact.md) |
| 10 | Mở rộng kiến thức | [Bài 21: JMeter/performance testing](Thang-03-CICD-Portfolio/Tuan-10-Mo-Rong-Kien-Thuc/Bai-21-JMeter-Performance-Testing.md)<br>[Bài 22: OWASP Top 10 + ôn tập Selenium](Thang-03-CICD-Portfolio/Tuan-10-Mo-Rong-Kien-Thuc/Bai-22-OWASP-Top10-Selenium-On-Tap.md) |
| 11 | Portfolio Project | [Bài 23: Xây dựng portfolio project](Thang-03-CICD-Portfolio/Tuan-11-Portfolio-Project/Bai-23-Xay-Dung-Portfolio-Project.md) |
| 12 | Ôn tập & phỏng vấn | [Bài 24: Ôn tập tổng hợp + luyện phỏng vấn](Thang-03-CICD-Portfolio/Tuan-12-On-Tap-Phong-Van/Bai-24-On-Tap-Tong-Hop-Phong-Van.md) |

## Bảng theo dõi tiến độ

| Tuần | Deliverable | Trạng thái |
|---|---|---|
| 1 | 10+ bài tập nhỏ trên GitHub | ☐ |
| 2 | 1 class quản lý dữ liệu hoàn chỉnh (vd Product) | ☐ |
| 3 | Repo cá nhân có commit history rõ ràng | ☐ |
| 4 | 15+ query mẫu (JOIN, subquery...) | ☐ |
| 5-6 | Bộ test UI cơ bản chạy được bằng Playwright + Pytest | ☐ |
| 7 | Framework có cấu trúc POM chuẩn + report tự động | ☐ |
| 8 | 10+ test case API tự động | ☐ |
| 9 | Pipeline CI/CD chạy tự động khi push code | ☐ |
| 10 | Hiểu JMeter + OWASP cơ bản, biết đọc code Selenium | ☐ |
| 11 | Portfolio project hoàn chỉnh trên GitHub (README + report) | ☐ |
| 12 | Sẵn sàng demo project + trả lời phỏng vấn theo JD | ☐ |

## Sau 3 tháng, bạn sẽ đối chiếu được với JD như sau

- ✅ Automation framework: Python + Playwright + Pytest (POM)
- ✅ API testing: Postman thủ công + tự động hóa bằng `requests`/Playwright APIRequestContext
- ✅ SQL: đủ để chuẩn bị và kiểm tra test data
- ✅ CI/CD: GitHub Actions chạy test tự động
- ✅ Nice-to-have: hiểu JMeter (performance), OWASP Top 10 (security), đọc hiểu Selenium cơ bản
- ✅ Portfolio project + repo GitHub làm bằng chứng khi phỏng vấn
