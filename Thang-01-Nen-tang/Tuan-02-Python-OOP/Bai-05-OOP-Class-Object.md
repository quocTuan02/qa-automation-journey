# Bài 05: Lập trình hướng đối tượng (OOP) cơ bản — Class, Object

**Tháng 1 – Tuần 2** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Hiểu và viết được `class` cơ bản. **Rất quan trọng**: Page Object Model (POM) — cấu trúc bắt buộc của mọi automation framework — được xây hoàn toàn bằng class.

## 📘 Nội dung học
1. **Class & Object**: `class TenClass:`, khởi tạo object.
2. **`__init__`** (constructor) và **`self`**: vì sao mọi method cần `self`.
3. **Thuộc tính (attribute)** và **phương thức (method)** của class.
4. **Kế thừa (inheritance)** cơ bản: class con kế thừa class cha bằng `class Con(Cha):`, dùng `super()`.
5. Liên hệ QA: 1 "Page" trong Playwright (vd `LoginPage`) sẽ là 1 class, mỗi hành động trên trang (nhập username, click login) sẽ là 1 method.

## 📚 Tài liệu tham khảo
- [Python.org – Classes](https://docs.python.org/3/tutorial/classes.html)
- [Real Python – OOP in Python 3](https://realpython.com/python3-object-oriented-programming/) (đọc kỹ, đây là bài rất hay và đủ dùng)
- [W3Schools – Python Classes/Objects](https://www.w3schools.com/python/python_classes.asp)

## ✍️ Bài tập
1. Viết class `Product` có thuộc tính `name`, `price`, `quantity`.
   - Method `total_value()` trả về `price * quantity`.
   - Method `apply_discount(percent)` giảm giá theo %.
2. Viết class `Student` quản lý điểm số: thuộc tính `name`, list `scores`; method `average()` tính điểm trung bình, method `add_score(score)` thêm điểm mới.
3. Tạo class `Animal` với method `speak()`, sau đó tạo class `Dog(Animal)` và `Cat(Animal)` kế thừa và override `speak()` khác nhau — để hiểu bản chất kế thừa/override (sẽ gặp lại khi các Page kế thừa 1 `BasePage` chung).
4. Đọc dữ liệu từ 1 list dict (mô phỏng đọc từ CSV) vào danh sách các object `Product`, in ra tổng giá trị kho hàng.
