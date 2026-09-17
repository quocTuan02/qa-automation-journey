# Bài 21: JMeter — Performance/Load Testing cơ bản

**Tháng 3 – Tuần 10** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Đáp ứng phần "Nên có" của JD: *"kinh nghiệm sử dụng các công cụ kiểm thử hiệu năng hoặc tải như JMeter, Locust hoặc Gatling"*. Ở mức 3 tháng, mục tiêu là **hiểu khái niệm và làm được 1 test plan cơ bản**, không cần chuyên sâu.

## 📘 Nội dung học
1. **Khái niệm**: performance testing vs load testing vs stress testing — khác gì với functional testing bạn đã quen.
2. **JMeter cơ bản**: cài đặt, giao diện, khái niệm **Thread Group** (mô phỏng số lượng user ảo), **Sampler** (HTTP Request), **Listener** (xem kết quả: response time, throughput).
3. Tạo 1 **Test Plan** đơn giản: gửi HTTP request tới 1 API demo, chạy với vài chục "user ảo" cùng lúc, quan sát kết quả.
4. (Biết sơ qua) **Locust/Gatling**: khác JMeter ở chỗ viết test bằng code (Locust dùng Python) thay vì kéo-thả GUI — biết tên và mục đích là đủ.

## 📚 Tài liệu tham khảo
- [Apache JMeter – User's Manual (Getting Started)](https://jmeter.apache.org/usermanual/get-started.html)
- [BlazeMeter – JMeter Tutorial for Beginners](https://www.blazemeter.com/blog/jmeter-tutorial)
- [Locust Docs](https://locust.io/) (đọc lướt phần "Quickstart" để biết khác gì JMeter)

## ✍️ Bài tập
1. Cài JMeter, tạo 1 Test Plan với Thread Group cấu hình 10 user ảo, 1 HTTP Request Sampler gọi `GET https://reqres.in/api/users`.
2. Thêm Listener "View Results Tree" và "Summary Report", chạy test, quan sát response time trung bình, số request thành công/thất bại.
3. Tăng số lượng user ảo lên 50-100, quan sát response time thay đổi thế nào — ghi nhận nhận xét ngắn (giống viết 1 báo cáo hiệu năng đơn giản).
4. Viết 1 đoạn ngắn (~5 dòng) giải thích: nếu test hiệu năng phát hiện response time tăng bất thường khi tăng tải, bạn sẽ báo cáo và trao đổi với team như thế nào (liên hệ JD phần "truyền đạt các rủi ro").
