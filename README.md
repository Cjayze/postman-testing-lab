# Báo cáo thực hành kiểm thử API với Postman

## 1. Giới thiệu

Postman hỗ trợ tạo và gửi HTTP request, kiểm tra response, tổ chức request thành collection và tái sử dụng cấu hình bằng environment variables. Bài thực hành này dùng Postman để gọi API mẫu, kiểm thử các phương thức HTTP cơ bản và xem dữ liệu thời tiết.

## 2. Công cụ và tài liệu tham khảo

- Postman Desktop/Web và Newman để chạy collection tự động từ dòng lệnh.
- [Video hướng dẫn Postman theo yêu cầu bài tập](https://www.youtube.com/watch?v=MFxk5BZulVU).
- [Postman Learning Center](https://learning.postman.com/docs/).
- [Hướng dẫn viết Postman test scripts](https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts/).
- [JSONPlaceholder Guide](https://jsonplaceholder.typicode.com/guide/).
- [Open-Meteo API](https://open-meteo.com/en/docs).

## 3. Kiểm thử API cơ bản

Collection [`LAB7.postman_collection.json`](postman/LAB7.postman_collection.json) gồm các request sau:

| Phương thức | Endpoint | Mục đích | Kết quả mong đợi |
| --- | --- | --- | --- |
| GET | `/posts/1` | Đọc bài viết có ID 1 | HTTP 200 và JSON bài viết hợp lệ |
| GET | `/posts?userId=1` | Lọc bài viết theo người dùng | HTTP 200 và các phần tử đều thuộc user 1 |
| POST | `/posts` | Gửi dữ liệu tạo bài viết | HTTP 201 và response khớp dữ liệu gửi |
| PUT | `/posts/1` | Gửi dữ liệu cập nhật bài viết | HTTP 200 và response khớp dữ liệu cập nhật |
| DELETE | `/posts/1` | Gửi yêu cầu xóa bài viết | HTTP 200 và response rỗng |

JSONPlaceholder là API giả lập phục vụ học tập: POST, PUT và DELETE trả response mô phỏng, không thay đổi dữ liệu lưu trữ lâu dài.

## 4. Kiểm thử response và sử dụng biến

Các request có Postman Tests để kiểm tra status code, kiểu dữ liệu JSON và nội dung response. URL cơ sở được cấu hình thành biến `{{baseUrl}}`, giúp thay đổi máy chủ API ở một nơi thay vì sửa từng request.

Environment [`LAB7.postman_environment.json`](postman/LAB7.postman_environment.json) cung cấp `baseUrl`, `weatherUrl`, `latitude` và `longitude`. Chọn environment **LAB7 - JSONPlaceholder** trong Postman trước khi chạy collection.

## 5. Thực hành API thời tiết

Request `GET /v1/forecast` gọi Open-Meteo để lấy nhiệt độ và tốc độ gió hiện tại tại TP. Hồ Chí Minh. Tọa độ và URL API được lấy từ environment. Endpoint này không yêu cầu API key.

Kết quả được kiểm tra bằng các assertion: HTTP 200, có đối tượng dữ liệu thời tiết hiện tại, nhiệt độ và tốc độ gió là số, và đơn vị nhiệt độ có trong response.

## 6. Cách chạy trong Postman

1. Chọn **Import** và import collection cùng environment trong thư mục `postman/`.
2. Chọn environment **LAB7 - JSONPlaceholder**.
3. Mở collection **LAB7 - JSONPlaceholder API Testing**, chọn **Run** và chạy toàn bộ request.
4. Kiểm tra trạng thái từng request và số assertion đạt/thất bại trong kết quả Collection Runner.

Nếu đã import phiên bản collection cũ, hãy import lại hai tệp mới nhất trong repo và chọn thay thế bản cũ (hoặc xóa collection/environment cũ trước khi import).

## 7. Kết quả chạy

Collection đã được chạy bằng Newman. Kết quả chi tiết được lưu ở [`results/newman-run.json`](results/newman-run.json).

| Request | Assertion đạt | Assertion lỗi | Kết quả |
| --- | ---: | ---: | --- |
| `GET /posts/1` | 2 | 0 | Đạt |
| `GET /posts?userId=1` | 2 | 0 | Đạt |
| `POST /posts` | 2 | 0 | Đạt |
| `PUT /posts/1` | 2 | 0 | Đạt |
| `DELETE /posts/1` | 2 | 0 | Đạt |
| `GET /v1/forecast` (Open-Meteo) | 2 | 0 | Đạt |

**Tổng kết:** 6 request, 12 assertion đạt, 0 assertion lỗi trong lần chạy Newman gần nhất.

## 8. Hình ảnh kết quả trên Postman

Sau khi import phiên bản mới và chạy đủ sáu request trên Postman Desktop/Web, chụp một ảnh Collection Runner thể hiện danh sách request và kết quả tổng thể. Lưu ảnh thật tại `screenshots/collection-run.png`, rồi bỏ dấu chú thích để hiện ảnh trong README:

```markdown
<!-- ![Kết quả chạy collection trên Postman](screenshots/collection-run.png) -->
```

## 9. Nhận xét

Bài thực hành giúp làm quen với GET, POST, PUT và DELETE, cách tổ chức request trong collection, kiểm tra response bằng assertion và tái sử dụng cấu hình bằng environment variables. Có thể bổ sung các API khác vào collection, nhưng cần cập nhật test tương ứng để xác nhận status code và dữ liệu trả về.
