# Bài 02: Cấu trúc điều khiển (if/else) và vòng lặp (for/while)

**Tháng 1 – Tuần 1** | Thời lượng gợi ý: 2 ngày

## 🎯 Mục tiêu
- Điều khiển luồng chương trình bằng điều kiện.
- Lặp lại thao tác bằng `for` và `while` — nền tảng để sau này lặp qua danh sách test case, test data.

## 📘 Nội dung học
1. **Câu lệnh điều kiện**: `if`, `elif`, `else`, điều kiện lồng nhau.
2. **Vòng lặp `for`**: lặp qua `range()`, lặp qua chuỗi/list.
3. **Vòng lặp `while`**: điều kiện dừng, tránh vòng lặp vô hạn.
4. **Điều khiển vòng lặp**: `break`, `continue`, `pass`.
5. Liên hệ thực tế QA: dùng vòng lặp để chạy lại 1 hành động (vd retry) hoặc kiểm tra danh sách phần tử trên UI sau này.

## 📚 Tài liệu tham khảo
- [Python.org – More Control Flow Tools](https://docs.python.org/3/tutorial/controlflow.html)
- [W3Schools – Python If...Else](https://www.w3schools.com/python/python_conditions.asp)
- [W3Schools – Python For Loops](https://www.w3schools.com/python/python_for_loops.asp) / [While Loops](https://www.w3schools.com/python/python_while_loops.asp)
- Luyện tập online: [HackerRank – Python (Easy)](https://www.hackerrank.com/domains/python)

## ✍️ Bài tập
1. Viết chương trình kiểm tra 1 số nhập vào là số nguyên tố hay không.
2. Viết chương trình tính giai thừa của n (n nhập từ bàn phím) bằng vòng lặp.
3. Viết chương trình đảo ngược 1 chuỗi (không dùng slicing `[::-1]`, dùng vòng lặp).
4. Viết chương trình in ra các số chẵn từ 1 đến 100, dùng `continue` để bỏ qua số lẻ.
5. Viết chương trình đoán số: máy chọn ngẫu nhiên 1 số từ 1-100 (`import random`), người dùng nhập số đoán, chương trình lặp và gợi ý "quá lớn/quá nhỏ" đến khi đoán đúng thì `break`.
