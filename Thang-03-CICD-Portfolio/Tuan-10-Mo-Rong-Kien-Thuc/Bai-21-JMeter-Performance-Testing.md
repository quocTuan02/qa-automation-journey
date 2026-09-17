# Bài 21: JMeter — Performance/Load Testing cơ bản

**Tháng 3 – Tuần 10** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Đáp ứng phần "Nên có" của JD: *"kinh nghiệm sử dụng các công cụ kiểm thử hiệu năng hoặc tải như JMeter, Locust hoặc Gatling"*. Ở mức 3 tháng, mục tiêu là **hiểu khái niệm và làm được 1 test plan cơ bản**, không cần chuyên sâu.

## 📘 Nội dung học
1. **Khái niệm**: functional testing (bạn đã quen) trả lời câu hỏi "tính năng có đúng không", còn performance/load/stress testing trả lời câu hỏi "hệ thống có **chịu tải tốt** không". Ba khái niệm hay bị nhầm:
   - **Performance testing**: đo tốc độ/độ ổn định hệ thống ở tải bình thường.
   - **Load testing**: tăng dần số lượng user để xem hệ thống chịu được bao nhiêu mà vẫn ổn.
   - **Stress testing**: cố tình đẩy tải vượt xa mức bình thường để xem hệ thống "vỡ" ở đâu và phục hồi thế nào.

   *Ví dụ liên hệ:* API `reqres.in` bình thường trả về trong 200ms với 1 user — performance testing hỏi "vẫn 200ms không nếu có 50 user gọi cùng lúc?", stress testing hỏi "nếu 5000 user gọi cùng lúc thì server sập ở đâu?".

2. **JMeter cơ bản**: cài đặt, giao diện, các khối chính:
   - **Thread Group**: mô phỏng số lượng "user ảo" (mỗi thread = 1 user đang thao tác), cấu hình gồm số thread, ramp-up (thời gian để tất cả thread bắt đầu chạy), số lần lặp.
   - **Sampler** (vd HTTP Request): mỗi sampler là 1 hành động cụ thể user ảo thực hiện — ở đây là 1 request gọi API.
   - **Listener**: nơi xem kết quả sau khi chạy — bảng số liệu hoặc biểu đồ.

   *Ví dụ cấu hình Thread Group để test `GET /api/users` của reqres.in:*

   | Thông số | Giá trị | Ý nghĩa |
   |---|---|---|
   | Number of Threads (users) | 10 | Có 10 "user ảo" cùng gọi API |
   | Ramp-up period (seconds) | 5 | Trong 5 giây, cả 10 user lần lượt bắt đầu (không bùng nổ cùng lúc) |
   | Loop Count | 3 | Mỗi user lặp lại request này 3 lần |
   | HTTP Request Sampler | `GET https://reqres.in/api/users?page=2` | Hành động mà mỗi user ảo thực hiện |

3. Tạo 1 **Test Plan** đơn giản: gói toàn bộ Thread Group + Sampler + Listener vào 1 file `.jmx`, chạy và đọc kết quả từ **Listener**:
   - "View Results Tree" — xem chi tiết từng request (status code, response body) — hữu ích khi debug.
   - "Summary Report" — xem tổng hợp: `Average` (response time trung bình), `Throughput` (số request xử lý được mỗi giây), `Error %` (tỉ lệ lỗi).

   *Ví dụ đọc kết quả Summary Report:*
   ```text
   Label        # Samples   Average   Min   Max   Error %   Throughput
   GET /users   30          180 ms    120   350   0.00%     45.2/sec
   ```
   → đọc như sau: 30 request đã chạy, trung bình mất 180ms, không có request nào lỗi, hệ thống xử lý được ~45 request/giây.

4. (Biết sơ qua) **Locust/Gatling**: khác JMeter ở chỗ viết test bằng code thay vì kéo-thả GUI — Locust dùng Python (rất hợp vì bạn đã học Python), Gatling dùng Scala.

   *Ví dụ 1 test Locust ngắn (chỉ để nhận diện cú pháp, không cần thực hành sâu):*
   ```python
   from locust import HttpUser, task, between

   class ApiUser(HttpUser):
       wait_time = between(1, 2)   # mỗi user nghỉ 1-2s giữa các lần gọi

       @task
       def get_users(self):
           self.client.get("/api/users?page=2")
   ```

## 📚 Tài liệu tham khảo
- [Apache JMeter – User's Manual (Getting Started)](https://jmeter.apache.org/usermanual/get-started.html)
- [BlazeMeter – JMeter Tutorial for Beginners](https://www.blazemeter.com/blog/jmeter-tutorial)
- [Locust Docs](https://locust.io/) (đọc lướt phần "Quickstart" để biết khác gì JMeter)

## ✍️ Bài tập
1. Cài JMeter, tạo 1 Test Plan với Thread Group cấu hình 10 user ảo, 1 HTTP Request Sampler gọi `GET https://reqres.in/api/users`.
2. Thêm Listener "View Results Tree" và "Summary Report", chạy test, quan sát response time trung bình, số request thành công/thất bại.
3. Tăng số lượng user ảo lên 50-100, quan sát response time thay đổi thế nào — ghi nhận nhận xét ngắn (giống viết 1 báo cáo hiệu năng đơn giản).
4. Viết 1 đoạn ngắn (~5 dòng) giải thích: nếu test hiệu năng phát hiện response time tăng bất thường khi tăng tải, bạn sẽ báo cáo và trao đổi với team như thế nào (liên hệ JD phần "truyền đạt các rủi ro").
