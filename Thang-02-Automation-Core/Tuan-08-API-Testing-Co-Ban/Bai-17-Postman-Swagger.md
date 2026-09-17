# Bài 17: API Testing thủ công — Postman & đọc Swagger

**Tháng 2 – Tuần 8** | Thời lượng gợi ý: 3 ngày

## 🎯 Mục tiêu
- Test API bằng tay trước khi tự động hóa — JD yêu cầu rõ *"có kinh nghiệm kiểm thử API"* và *"thực hiện kiểm thử API bằng các công cụ như Postman hoặc Swagger"*.

## 📘 Nội dung học
1. **Kiến thức HTTP/REST cơ bản**: mỗi API là 1 "địa chỉ" (URL) mà client gọi tới theo 1 **method** thể hiện ý định (lấy dữ liệu, tạo mới, sửa, xóa...), server trả về **status code** cho biết kết quả, và **body** (thường là JSON) chứa dữ liệu thật.
   - `GET` = lấy dữ liệu, `POST` = tạo mới, `PUT`/`PATCH` = sửa, `DELETE` = xóa.
   - `2xx` = thành công (`200 OK`, `201 Created`), `4xx` = lỗi do client (`400 Bad Request`, `401 Unauthorized`, `404 Not Found`), `5xx` = lỗi do server (`500 Internal Server Error`).
   - **Query param**: tham số gắn sau dấu `?` trong URL (vd `?page=2`). **Path param**: tham số nằm ngay trong đường dẫn (vd `/api/users/2`, số `2` là path param).

   *Ví dụ minh họa:*
   ```text
   GET https://reqres.in/api/users?page=2        <- query param "page"
   GET https://reqres.in/api/users/2              <- path param "2" (id của user)
   POST https://reqres.in/api/users               <- tạo user mới, dữ liệu nằm trong body JSON
   ```

2. **Postman**: tạo 1 request bằng cách chọn method + gõ URL + bấm Send; nhóm nhiều request liên quan vào 1 **Collection** (vd Collection "User API" gồm các request GET/POST/PUT/DELETE user); dùng **Environment variable** để không phải sửa tay URL khi đổi môi trường test (dev/staging/production).

   *Ví dụ:* tạo Environment "Dev" với biến `base_url = https://reqres.in`, sau đó mọi request trong Collection viết là:
   ```text
   GET {{base_url}}/api/users?page=2
   ```
   Khi đổi sang môi trường khác, chỉ cần đổi giá trị `base_url` trong Environment, không phải sửa từng request.

3. **Postman Tests tab**: mỗi request có thể gắn kèm 1 đoạn script JavaScript chạy tự động sau khi nhận response, dùng để tự động kiểm tra (assert) kết quả trả về thay vì nhìn bằng mắt.

   ```javascript
   // Viết trong tab "Tests" của request GET /api/users?page=2
   pm.test("Status code la 200", function () {
       pm.response.to.have.status(200);
   });

   pm.test("Response co field data la mang", function () {
       const jsonData = pm.response.json();
       pm.expect(jsonData.data).to.be.an('array');
   });

   pm.test("Response time duoi 1000ms", function () {
       pm.expect(pm.response.responseTime).to.be.below(1000);
   });
   ```
   Sau khi bấm Send, tab "Test Results" sẽ hiện rõ từng assertion PASS ✅ hay FAIL ❌.

4. **Đọc tài liệu Swagger/OpenAPI**: Swagger UI hiển thị trực quan toàn bộ endpoint của 1 API — mỗi endpoint liệt kê rõ: field nào bắt buộc, kiểu dữ liệu, response mẫu — giúp bạn biết chính xác cần gửi gì và mong đợi nhận lại gì **trước khi** viết bất kỳ test nào.

   *Ví dụ đọc docs endpoint `POST /pet` trên Swagger Petstore:*
   ```json
   // Request body mẫu Swagger cung cấp
   {
     "id": 0,
     "name": "doggie",        // field bắt buộc (required), kiểu string
     "photoUrls": ["string"], // field bắt buộc, kiểu array of string
     "status": "available"    // enum: available | pending | sold
   }
   ```
   Từ đây bạn biết ngay: nếu test thiếu field `name` hoặc `photoUrls`, API phải trả lỗi `400` — đó chính là 1 test case cần viết.

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
