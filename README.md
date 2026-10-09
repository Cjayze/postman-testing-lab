# Bài thực hành Postman: Kiểm thử API JSONPlaceholder

## 1. Mục tiêu

- Làm quen với Postman và quy trình gửi request HTTP.
- Kiểm thử các API endpoint bằng phương thức GET, POST và PUT.
- Viết assertion bằng Postman Tests để kiểm tra status code, dữ liệu JSON và nội dung phản hồi.
- Lưu collection để có thể chạy lại và chia sẻ kết quả.

## 2. Tài liệu tham khảo

- Video hướng dẫn do đề bài cung cấp: [Học Postman](https://www.youtube.com/watch?v=MFxk5BZulVU).
- Tài liệu chính thức: [Postman Learning Center](https://learning.postman.com/docs/).
- Tài liệu viết test script: [Write scripts to test API response data](https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts/).
- API dùng trong bài: [JSONPlaceholder Guide](https://jsonplaceholder.typicode.com/guide/).

## 3. Công cụ và API

- Postman Desktop hoặc Postman Web.
- API mẫu: `https://jsonplaceholder.typicode.com`.
- Đây là API giả lập phục vụ học tập; thao tác tạo/cập nhật dữ liệu không lưu thay đổi thật trên máy chủ.

## 4. Collection

Collection Postman nằm tại [`postman/LAB7.postman_collection.json`](postman/LAB7.postman_collection.json); environment mẫu nằm tại [`postman/LAB7.postman_environment.json`](postman/LAB7.postman_environment.json).

Collection gồm bốn request:

| Request | Mục đích | Kết quả mong đợi |
| --- | --- | --- |
| `GET /posts/1` | Đọc một bài viết | HTTP 200; `id` bằng 1; `userId` và `title` có dữ liệu |
| `GET /posts?userId=1` | Lọc bài viết theo người dùng | HTTP 200; phản hồi là mảng không rỗng; mọi phần tử có `userId` bằng 1 |
| `POST /posts` | Tạo bài viết giả lập | HTTP 201; dữ liệu trả về khớp với nội dung gửi lên |
| `PUT /posts/1` | Cập nhật bài viết giả lập | HTTP 200; dữ liệu trả về có tiêu đề và nội dung mới |

Mỗi request có các kiểm tra trong tab **Scripts > Post-response** (hoặc **Tests**, tùy phiên bản Postman).

## 5. Cách chạy

1. Mở Postman và chọn **Import**.
2. Import hai tệp trong thư mục `postman/`.
3. Chọn environment `LAB7 - JSONPlaceholder`.
4. Mở collection **LAB7 - JSONPlaceholder API Testing**, rồi chọn **Run**.
5. Chạy toàn bộ request trong Collection Runner.
6. Xem số assertion thành công/thất bại trong kết quả chạy. Mỗi request cần đạt tất cả assertion để xem là đạt.

## 6. Báo cáo kết quả

Collection đã được chạy bằng Newman (Postman CLI runtime) với environment mẫu. Lần chạy thực tế hoàn tất thành công, gồm 1 iteration, 4 request, 8 assertion đạt và 0 assertion thất bại. Tệp JSON kết quả được lưu tại [`results/newman-run.json`](results/newman-run.json).

| Request | Số assertion đạt | Số assertion thất bại | Kết luận |
| --- | ---: | ---: | --- |
| `GET /posts/1` | 2 | 0 | Đạt; HTTP 200 |
| `GET /posts?userId=1` | 2 | 0 | Đạt; HTTP 200 |
| `POST /posts` | 2 | 0 | Đạt; HTTP 201 |
| `PUT /posts/1` | 2 | 0 | Đạt; HTTP 200 |

## 7. Hình ảnh minh hoạ

Lần chạy đã thực hiện bằng Newman trên dòng lệnh, không phải giao diện Postman Desktop/Web; vì vậy chưa có ảnh chụp giao diện Postman. Để bổ sung ảnh theo yêu cầu nộp bài, import collection và environment ở mục 5 vào Postman, chạy cả collection bằng **Run**, rồi chụp kết quả thật từ màn hình:

1. Kết quả Collection Runner cho toàn bộ collection.
2. Kết quả chi tiết request `GET /posts/1`.
3. Kết quả chi tiết request `POST /posts`.

Lưu ảnh lần lượt vào `screenshots/collection-run.png`, `screenshots/get-post-1.png` và `screenshots/post-post.png`. Sau đó bỏ dấu chú thích ở các dòng dưới để hiện ảnh:

```markdown
<!-- ![Kết quả chạy toàn bộ collection](screenshots/collection-run.png) -->
<!-- ![Kết quả GET /posts/1](screenshots/get-post-1.png) -->
<!-- ![Kết quả POST /posts](screenshots/post-post.png) -->
```

## 8. Nhận xét

Qua bài thực hành, đã gửi request GET để đọc và lọc dữ liệu, POST để thử tạo mới và PUT để thử cập nhật. Các test script xác nhận status code và kiểm tra nội dung JSON trả về. JSONPlaceholder chỉ giả lập thao tác ghi; dữ liệu tạo/cập nhật không được lưu lâu dài.
