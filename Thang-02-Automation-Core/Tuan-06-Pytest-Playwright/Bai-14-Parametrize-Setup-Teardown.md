# Bài 14: Parametrize test + Setup/Teardown nâng cao

**Tháng 2 – Tuần 6** | Thời lượng gợi ý: 2-3 ngày + 1 ngày bài tập tổng hợp

## 🎯 Mục tiêu
- Chạy 1 test với nhiều bộ dữ liệu khác nhau (data-driven testing) — kỹ năng giúp viết ít code mà cover nhiều trường hợp, đúng tinh thần "chuẩn bị test data" trong JD.

## 📘 Nội dung học
1. **`@pytest.mark.parametrize`**: chạy 1 hàm test với nhiều tập giá trị đầu vào.
2. **Fixture scope**: `function` (mặc định), `module`, `session` — khi nào nên mở browser 1 lần dùng chung, khi nào mở mới mỗi test.
3. **Setup/Teardown nâng cao**: dùng `yield` trong fixture để vừa setup vừa teardown (vd: login trước mỗi test, logout sau mỗi test).
4. **Markers**: đánh dấu test (`@pytest.mark.smoke`, `@pytest.mark.regression`) để chạy chọn lọc bằng `pytest -m smoke`.

## 📚 Tài liệu tham khảo
- [Pytest Docs – Parametrize](https://docs.pytest.org/en/stable/how-to/parametrize.html)
- [Pytest Docs – Fixture finalization (yield)](https://docs.pytest.org/en/stable/how-to/fixtures.html#teardown-cleanup-aka-fixture-finalization)
- [Pytest Docs – Marks](https://docs.pytest.org/en/stable/how-to/mark.html)

## ✍️ Bài tập
1. Viết lại case "login sai" bằng `parametrize` với ít nhất 4 bộ dữ liệu (sai username, sai password, để trống cả 2, tài khoản bị khóa `locked_out_user` — có sẵn trên saucedemo) — assert đúng thông báo lỗi tương ứng mỗi trường hợp.
2. Viết 1 fixture `logged_in_page` dùng `yield`: setup = login vào saucedemo, sau `yield` = không cần teardown đặc biệt (Playwright tự đóng), nhưng thử thêm log "Test kết thúc" để hiểu rõ thứ tự chạy.
3. Đánh marker `@pytest.mark.smoke` cho các test quan trọng nhất (login thành công, thêm giỏ hàng), thử chạy riêng `pytest -m smoke`.
4. **Bài tập tổng hợp tuần 6**: Viết bộ test hoàn chỉnh cho luồng "thêm sản phẩm vào giỏ hàng" trên saucedemo: dùng fixture `logged_in_page`, parametrize với ít nhất 3 sản phẩm khác nhau, assert đúng tên/giá/số lượng trong giỏ hàng.
