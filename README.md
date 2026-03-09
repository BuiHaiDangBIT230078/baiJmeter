# Kiểm thử hiệu năng website bằng JMeter

## 1. Giới thiệu

Bài thực hành này sử dụng **Apache JMeter** để thực hiện kiểm thử hiệu năng của website **Wikipedia**.

Mục tiêu của bài kiểm thử:

* Hiểu cách sử dụng JMeter để mô phỏng nhiều người dùng truy cập website.
* Thiết kế các kịch bản kiểm thử với các mức tải khác nhau.
* Thu thập và phân tích các chỉ số hiệu năng như **Response Time, Throughput và Error Rate**.

Website được chọn để kiểm thử:

```
https://www.wikipedia.org
```

Công cụ sử dụng:

* Apache JMeter
* GitHub để lưu trữ kết quả kiểm thử

---

# 2. Cấu hình kiểm thử

Trong JMeter, một **Test Plan** được tạo với **3 Thread Group** để mô phỏng các tình huống truy cập khác nhau.

## 2.1 HTTP Request Defaults

Cấu hình chung cho tất cả request:

| Thuộc tính  | Giá trị                                       |
| ----------- | --------------------------------------------- |
| Protocol    | https                                         |
| Server Name | [www.wikipedia.org](http://www.wikipedia.org) |

---

# 3. Các kịch bản kiểm thử

## 3.1 Thread Group 1 – Kịch bản cơ bản

Mục đích: mô phỏng số lượng nhỏ người dùng truy cập trang chủ.

Cấu hình:

| Thuộc tính        | Giá trị  |
| ----------------- | -------- |
| Number of Threads | 10 users |
| Loop Count        | 5        |
| Request           | GET /    |

Hành vi người dùng:

* Người dùng truy cập trang chủ của website.

---

## 3.2 Thread Group 2 – Kịch bản tải nặng

Mục đích: mô phỏng nhiều người dùng truy cập đồng thời.

Cấu hình:

| Thuộc tính        | Giá trị    |
| ----------------- | ---------- |
| Number of Threads | 50 users   |
| Ramp-up Period    | 30 seconds |

Request được gửi:

* GET `/`
* GET `/wiki/Technology`

Hành vi người dùng:

* Người dùng truy cập trang chủ.
* Sau đó truy cập một bài viết trên website.

---

## 3.3 Thread Group 3 – Kịch bản tùy chỉnh

Mục đích: mô phỏng người dùng truy cập nhiều nội dung khác nhau.

Cấu hình:

| Thuộc tính        | Giá trị    |
| ----------------- | ---------- |
| Number of Threads | 20 users   |
| Duration          | 60 seconds |

Request:

* GET `/wiki/Technology`
* GET `/wiki/Computer`

Hành vi người dùng:

* Người dùng truy cập nhiều trang bài viết khác nhau.

---

# 4. Thu thập kết quả

Các listener được sử dụng:

* View Results Tree
* Summary Report
* Graph Results

Các chỉ số được thu thập:

* **Response Time**
* **Throughput**
* **Error Rate**

---

# 5. Phân tích kết quả

Sau khi chạy kiểm thử, các kết quả cho thấy:

* Response Time trung bình ổn định khi số lượng người dùng thấp.
* Khi số lượng người dùng tăng lên (Thread Group 2), thời gian phản hồi tăng.
* Throughput cho thấy hệ thống có thể xử lý nhiều request mỗi giây.
* Error Rate thấp cho thấy website hoạt động ổn định.

---

# 6. Kết luận

Qua bài kiểm thử hiệu năng với JMeter:

* Website có thể xử lý nhiều request đồng thời.
* Thời gian phản hồi tăng khi tải hệ thống tăng.
* JMeter là công cụ hiệu quả để mô phỏng tải và phân tích hiệu năng hệ thống.

---

# 7. Tài liệu tham khảo

* https://jmeter.apache.org
* https://www.wikipedia.org
