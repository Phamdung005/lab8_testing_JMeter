# Kiểm thử hiệu năng API bằng Apache JMeter

## 1. Giới thiệu

Dự án sử dụng **Apache JMeter 5.6.3** để thực hiện kiểm thử hiệu năng API bằng cách gửi nhiều HTTP request đến một API công khai, thu thập thời gian phản hồi và đánh giá kết quả.

API được sử dụng trong bài thực hành là DummyJSON Posts API.

## 2. Mục tiêu

- Làm quen với công cụ Apache JMeter.
- Xây dựng kịch bản kiểm thử HTTP GET.
- Mô phỏng nhiều request đến API.
- Theo dõi số lượng request thành công và thất bại.
- Phân tích thời gian phản hồi và Throughput.
- Đánh giá kết quả kiểm thử trong điều kiện thực nghiệm.

## 3. Công cụ sử dụng

| Công cụ | Mục đích |
|---|---|
| Apache JMeter 5.6.3 | Thực hiện kiểm thử hiệu năng |
| Java | Môi trường chạy JMeter |
| DummyJSON | API dùng trong bài thực hành |

## 4. API được kiểm thử

- **Endpoint:** `https://dummyjson.com/posts?limit=3`
- **Method:** `GET`
- **Tham số:** `limit=3`
- **Mục đích:** Lấy danh sách bài viết từ API.

Request sử dụng phương thức GET để truy xuất dữ liệu. Tham số `limit=3` yêu cầu API trả về tối đa ba bài viết.

## 5. Kịch bản kiểm thử

Kịch bản được xây dựng trong Apache JMeter với các thành phần:

- **Thread Group:** Quản lý các luồng người dùng ảo và số lần lặp.
- **HTTP Request:** Gửi request GET đến DummyJSON Posts API.
- **View Results Tree:** Kiểm tra kết quả từng request và dữ liệu phản hồi.
- **Summary Report:** Tổng hợp các chỉ số hiệu năng.

### Quy trình thực hiện

1. Tạo Test Plan trong JMeter.
2. Thêm Thread Group.
3. Cấu hình HTTP Request đến DummyJSON.
4. Thêm các Listener để theo dõi kết quả.
5. Chạy kịch bản kiểm thử.
6. Thu thập và phân tích số liệu từ Summary Report.

## 6. Kết quả kiểm thử

Kết quả được ghi nhận từ Summary Report của Apache JMeter.

| Chỉ số | Kết quả |
|---|---:|
| Tổng số request (Samples) | 100 |
| Số request thành công | 100 |
| Số request thất bại | 0 |
| Tỷ lệ lỗi (Error %) | 0,00% |
| Thời gian phản hồi trung bình (Average) | 314 ms |
| Thời gian phản hồi nhỏ nhất (Min) | 238 ms |
| Thời gian phản hồi lớn nhất (Max) | 1.625 ms |
| Độ lệch chuẩn (Std. Dev.) | 171,58 ms |
| Throughput | 13,9 request/giây |
| Tốc độ nhận dữ liệu | 37,30 KB/s |
| Kích thước phản hồi trung bình | 2.749,9 bytes |

### Ảnh kết quả

#### View Results Tree

Ảnh này thể hiện các request được gửi đến API và dữ liệu JSON nhận được từ máy chủ.

<img width="1280" height="763" alt="image" src="https://github.com/user-attachments/assets/e9c496f9-d5d3-44ad-a25b-12a5d10e2c88" />



#### Summary Report

Ảnh này thể hiện số lượng request, thời gian phản hồi, tỷ lệ lỗi và Throughput sau khi chạy kiểm thử.

<img width="1279" height="761" alt="image" src="https://github.com/user-attachments/assets/9e98a8e2-548c-463d-a93d-732b1caa3dbe" />


## 7. Phân tích kết quả

### 7.1. Tỷ lệ thành công

JMeter ghi nhận 100 request và tỷ lệ lỗi là 0,00%. Điều này cho thấy tất cả request trong lần chạy này đều được JMeter ghi nhận là thành công.

### 7.2. Thời gian phản hồi

Thời gian phản hồi trung bình đạt 314 ms. Request nhanh nhất mất 238 ms, trong khi request chậm nhất mất 1.625 ms.

Chênh lệch giữa thời gian phản hồi nhỏ nhất và lớn nhất cho thấy độ trễ có sự dao động trong quá trình kiểm thử. Độ lệch chuẩn đạt 171,58 ms, thể hiện mức phân tán của thời gian phản hồi quanh giá trị trung bình.

### 7.3. Throughput

Throughput đạt 13,9 request/giây. Đây là tốc độ xử lý request được ghi nhận trong điều kiện của lần kiểm thử này.

Throughput có thể thay đổi tùy theo cấu hình JMeter, máy chạy kiểm thử, chất lượng kết nối mạng và tình trạng của máy chủ API.

## 8. Kết luận

Trong lần kiểm thử này, DummyJSON Posts API xử lý thành công 100 request được ghi nhận bởi JMeter, với tỷ lệ lỗi bằng 0,00% và thời gian phản hồi trung bình 314 ms.

Kết quả cho thấy API phản hồi thành công trong phạm vi kịch bản đã thực hiện. Tuy nhiên, đây mới là kết quả của một lần kiểm thử với quy mô 100 request, chưa đủ để kết luận về khả năng chịu tải tối đa hoặc hiệu năng của API trong mọi điều kiện.

Để đánh giá toàn diện hơn, có thể thực hiện thêm các lần kiểm thử với nhiều mức tải khác nhau, so sánh kết quả giữa các lần chạy và theo dõi các chỉ số phần trăm thời gian phản hồi như Median và 90% Line.

## 9. Cấu trúc repository

```text
jmeter-api-performance/
├── README.md
├── API_Performance_Test.jmx
└── screenshots/
    ├── view-results-tree.png
    └── summary-report.png
```
