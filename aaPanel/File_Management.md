## File_Management

### Basic operation
- Các hoạt động cơ bản trên tệp tin bao gồm:

- Sao chép, dán, cắt, xóa, đổi tên, nén, làm mới, tạo tệp mới, tạo thư mục mới.

- Bảng điều khiển cung cấp các hoạt động cơ bản trên tệp tin đầy đủ, giống như quản lý tệp tin trên Windows. Bạn có thể nhấp chuột phải hoặc chọn tệp tin để thực hiện các hoạt động sao chép, cắt và các hoạt động khác trên tệp tin (xem hình ảnh):

![Imgur](https://i.imgur.com/ZIa99mk.png)

- Tạo File/Folder

![Imgur](https://i.imgur.com/xx5iirb.png)


### File upload
- Bạn có thể upload file hoặc thư mục

![Imgur](https://i.imgur.com/8qTY3E1.png)

Lưu ý:
- Đường dẫn tải lên là đường dẫn được hiển thị bởi trình quản lý tệp tin hiện tại.

- Nếu tệp đã được tải lên tồn tại, nó sẽ bị ghi đè.


### Permission Management
- Mỗi tệp hoặc thư mục trong Linux đều chứa quyền truy cập, quyết định ai có thể truy cập và cách truy cập các tệp và thư mục này.

- Khu vực quyền được chia thành ba phần: chủ sở hữu, nhóm người dùng và công cộng.

- Chủ sở hữu: Quyền hiện tại được chỉ định bởi chủ sở hữu.

- Quy tắc quyền, biểu thị đọc là 4, biểu thị ghi là 2, biểu thị thực thi là 1, 4 + 2 + 1 = 7. Số 7 biểu thị tất cả các quyền.

- Lưu ý: Hãy phân bổ quyền một cách hợp lý để tránh việc không thể truy cập tài nguyên trang web.

![Imgur](https://i.imgur.com/p3t3i3l.png)

![Imgur](https://i.imgur.com/RVrq3TH.png)


- Nếu bạn đặt quyền cho một thư mục và áp dụng nó cho các tệp con trong thư mục đó, chúng tôi sẽ mặc định hỏi bạn liệu bạn có muốn sao lưu quyền để hỗ trợ khôi phục khi có vấn đề với việc thiết lập quyền không.

### Recycle bin
- Thùng rác được kích hoạt mặc định.

- Hiển thị các tệp đã bị xóa hiện tại và cung cấp các chức năng như khôi phục, xóa vĩnh viễn và làm trống thùng rác.

- Mục đích của thùng rác là ngăn người dùng xóa tệp tin một cách vô tình, nhưng thực tế là tệp tin không bị xóa vĩnh viễn. Sau khi xóa tệp, các tệp nguồn được di chuyển đến thư mục thùng rác, vì vậy bạn cần phải xóa tệp tin một cách hoàn toàn. Sau khi đã xóa tệp tin, hãy xóa nó một cách hoàn toàn trong thùng rác.

Lưu ý:

- Vui lòng sử dụng cẩn thận khi làm trống thùng rác và thực hiện công cụ sau khi đã xác nhận rằng dữ liệu đã bị xóa mà không có lỗi.

![Imgur](https://i.imgur.com/jUYnwya.png)

