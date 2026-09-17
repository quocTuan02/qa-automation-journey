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
| 1 | Python cơ bản | Biến/kiểu dữ liệu/toán tử → Điều kiện/vòng lặp → Hàm |
| 2 | Python trung cấp + OOP | List/Dict/String nâng cao → Class/Object (OOP) → Exception/File I-O |
| 3 | Git & môi trường làm việc | Git/GitHub cơ bản → VSCode/venv/pip |
| 4 | SQL nâng cao cho tester | JOIN/GROUP BY/HAVING → Subquery/Aggregate/CASE WHEN |

### Tháng 2 — Automation Core (`Thang-02-Automation-Core/`)
| Tuần | Chủ đề | Bài học |
|---|---|---|
| 5 | Playwright cơ bản | Cài đặt + Locator → Actions/Assertions/Wait |
| 6 | Pytest + Playwright | Cấu trúc Pytest/Fixture → Parametrize/Setup-Teardown |
| 7 | Page Object Model | Khái niệm POM + refactor → Test report (pytest-html/Allure) |
| 8 | API Testing cơ bản | Postman/Swagger → Requests library + Pytest |

### Tháng 3 — CI/CD & Portfolio (`Thang-03-CICD-Portfolio/`)
| Tuần | Chủ đề | Bài học |
|---|---|---|
| 9 | CI/CD với GitHub Actions | Khái niệm CI/CD + YAML → Workflow + report artifact |
| 10 | Mở rộng kiến thức | JMeter/performance testing → OWASP Top 10 + ôn tập Selenium |
| 11 | Portfolio Project | Xây dựng project hoàn chỉnh (UI + API + CI/CD) |
| 12 | Ôn tập & phỏng vấn | Ôn tập tổng hợp + luyện phỏng vấn theo JD |

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
