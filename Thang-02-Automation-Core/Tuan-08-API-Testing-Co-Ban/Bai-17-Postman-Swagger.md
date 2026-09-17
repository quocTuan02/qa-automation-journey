# Bài 17: API Testing thủ công — Postman & đọc Swagger

**Tháng 2 – Tuần 8** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Test API bằng tay trước khi tự động hóa — JD yêu cầu rõ *"có kinh nghiệm kiểm thử API"* và *"thực hiện kiểm thử API bằng các công cụ như Postman hoặc Swagger"*.

## 📘 Nội dung học
1. **Kiến thức HTTP/REST cơ bản**: method (`GET/POST/PUT/PATCH/DELETE`), status code (`2xx/4xx/5xx` nghĩa là gì), header, body (JSON), query param vs path param.
2. **Postman**: tạo request, tạo **Collection**, dùng **Environment variable** (vd `{{base_url}}`) để tái sử dụng giữa các môi trường (dev/staging).
3. **Postman Tests tab**: viết assertion đơn giản bằng JavaScript có sẵn (`pm.test(...)`, `pm.response.to.have.status(200)`).
4. **Đọc tài liệu Swagger/OpenAPI**: hiểu request schema, response schema, các trường bắt buộc — kỹ năng đọc hiểu API contract trước khi viết test.

## 📚 Tài liệu tham khảo
- [Postman Learning Center – Getting Started](https://learning.postman.com/docs/getting-started/overview/)
- [MDN – HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [Swagger/OpenAPI – Docs](https://swagger.io/docs/specification/about/)
- API demo để luyện tập: [reqres.in](https://reqres.in) (đơn giản, không cần auth), [Swagger Petstore demo](https://petstore.swagger.io/) (có Swagger UI đầy đủ để luyện đọc docs)

## ✍️ Bài tập
1. Cài Postman, tạo Collection "QA Practice API", tạo request `GET https://reqres.in/api/users?page=2`, quan sát response.
2. Thêm request `POST https://reqres.in/api/users` với body JSON tạo user mới, kiểm tra status code trả về.
3. Viết ít nhất 3 assertion bằng `pm.test()` cho mỗi request (status code đúng, response có đúng field, response time hợp lý).
4. Tạo Environment với biến `base_url`, sửa lại toàn bộ request trong Collection dùng `{{base_url}}` thay vì hard-code URL.
5. Vào [Swagger Petstore](https://petstore.swagger.io/), đọc docs endpoint `POST /pet`, liệt kê ra giấy: field nào bắt buộc, kiểu dữ liệu từng field, response mẫu — rồi thử gọi thật request đó qua Swagger UI ("Try it out").
