# Bài 05: Lập trình hướng đối tượng (OOP) cơ bản — Class, Object

**Tháng 1 – Tuần 2** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Hiểu và viết được `class` cơ bản. **Rất quan trọng**: Page Object Model (POM) — cấu trúc bắt buộc của mọi automation framework — được xây hoàn toàn bằng class.

## 📘 Nội dung học

1. **Class & Object**: `class` là 1 "bản thiết kế" mô tả 1 loại đối tượng (có thuộc tính gì, làm được gì); `object` là 1 thực thể cụ thể được tạo ra từ bản thiết kế đó. Ví dụ: `class Product` là thiết kế chung "sản phẩm", còn `Product("Ao thun", 100)` là 1 sản phẩm cụ thể (object).

   ```python
   class Product:
       pass   # class rong, chua co gi

   san_pham_1 = Product()   # tao 1 object tu class Product
   ```

2. **`__init__`** (constructor) là method đặc biệt tự động chạy ngay khi 1 object được tạo ra, dùng để gán giá trị ban đầu cho object đó. **`self`** là tham số đầu tiên bắt buộc của mọi method trong class, đại diện cho "chính object đang được thao tác" — nhờ `self` mà mỗi object nhớ được dữ liệu riêng của nó.

   ```python
   class Product:
       def __init__(self, name, price):
           self.name = name       # gan gia tri vao rieng object nay
           self.price = price

   ao_thun = Product("Ao thun", 100)
   quan_jean = Product("Quan jean", 250)
   print(ao_thun.name, quan_jean.name)   # Ao thun Quan jean -> moi object nho du lieu rieng
   ```

3. **Thuộc tính (attribute)** là dữ liệu gắn với object (`self.name`, `self.price`), **phương thức (method)** là hành vi/hàm gắn với object đó (định nghĩa bằng `def` bên trong class, luôn có `self` là tham số đầu).

   ```python
   class Product:
       def __init__(self, name, price, quantity):
           self.name = name
           self.price = price
           self.quantity = quantity

       def total_value(self):              # method: hanh vi cua object
           return self.price * self.quantity

   ao_thun = Product("Ao thun", 100, 5)
   print(ao_thun.total_value())             # 500
   ```

4. **Kế thừa (inheritance)**: cho phép 1 class con dùng lại toàn bộ thuộc tính/method của class cha, chỉ cần viết thêm phần khác biệt — tránh lặp code giữa các class có nhiều điểm chung. `super().__init__(...)` gọi lại constructor của class cha.

   ```python
   class Animal:
       def __init__(self, name):
           self.name = name

       def speak(self):
           return "..."

   class Dog(Animal):                # Dog ke thua Animal
       def speak(self):              # override lai method speak
           return f"{self.name} sua: Gau gau!"

   class Cat(Animal):
       def speak(self):
           return f"{self.name} keu: Meo meo!"

   print(Dog("Mi").speak())    # Mi sua: Gau gau!
   print(Cat("Kitty").speak()) # Kitty keu: Meo meo!
   ```

5. **Liên hệ QA**: 1 "Page" trong Playwright (vd `LoginPage`) sẽ là 1 class, mỗi hành động trên trang (nhập username, click login) sẽ là 1 method — đây chính xác là mô hình bạn sẽ dùng ở Bài 15 (Page Object Model).

   ```python
   class LoginPage:
       def __init__(self, page):
           self.page = page   # "page" ở đây là đối tượng trình duyệt của Playwright

       def login(self, username, password):
           self.page.get_by_placeholder("Username").fill(username)
           self.page.get_by_placeholder("Password").fill(password)
           self.page.get_by_text("Login").click()

   # Cach dung sau nay trong test:
   # login_page = LoginPage(page)
   # login_page.login("standard_user", "secret_sauce")
   ```

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
