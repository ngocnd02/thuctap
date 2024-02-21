## Backing up and Restoration

- Với chức năng sao lưu và khôi phục dữ liệu do Plesk cung cấp, bạn có thể thực hiện những việc sau:
	- Sao lưu toàn bộ máy chủ.
	- Sao lưu tài khoản người dùng cá nhân với các trang web.
	- Sao lưu các đăng ký riêng lẻ.
	- Lên lịch sao lưu.
	- Khôi phục dữ liệu từ kho lưu trữ sao lưu.

### Backup
- Trước khi ta backup dữ liệu hãy tạo ra một số bài viết trong trang web của bạn để kiểm tra dữ liệu có được phục hồi sau khi ta restore hay không. 

![Imgur](https://i.imgur.com/Zpd2Ll1.png)

- Để backup dữ liệu ta truy cập vào tài khoản Plesk mà ta muốn backup, sau đó vào **Website & Domains** > **Backup & Restore** 

![Imgur](https://i.imgur.com/YpAvwp7.png)

- Ấn chọn **Backup**

![Imgur](https://i.imgur.com/mUTeX4c.png)

- Chọn những dữ liệu mà bạn muốn backup. 

![Imgur](https://i.imgur.com/m2vXEiA.png)


Trong đó: Plesk hỗ trợ 2 kiểu sao lưu là **Full** và **Incremental**
	- **Full**: Mỗi lần bạn tạo bản sao lưu, bản sao lưu sẽ bao gồm tất cả dữ liệu bất kể thời điểm dữ liệu được cập nhật lần cuối.

	- **Incremental**: Bản sao lưu incremental chỉ chứa dữ liệu đã được thay đổi kể từ thời điểm sao lưu được tạo trước đó.

Việc sử dụng các bản sao lưu incremental giúp giảm đáng kể thời lượng của thao tác sao lưu và dung lượng ổ đĩa bị chiếm giữ bởi các tệp sao lưu.

- Sau khi backup thành công sẽ xuất hiện 1 file backup vừa được tạo

![Imgur](https://i.imgur.com/ACHnbY3.png)


- Sau khi backup thành công, ta vào quản lý trang web và xóa tất cả các bài viết đi

![Imgur](https://i.imgur.com/eFkCsVW.png)


### Restore
- Vào **Website & Domain** > **Backup & Restore**, ta sẽ thấy những danh sách file backup mà ta đã tiến hành tạo, chọn một file backup mà ta muốn khôi phục

![Imgur](https://i.imgur.com/svF4yva.png)

- Tùy chọn các loại dữ liệu mà muốn khôi phục

![Imgur](https://i.imgur.com/qKqdDyx.png)

- Sau khi khôi phục thành công sẽ có thông báo

![Imgur](https://i.imgur.com/llLO9CL.png)

- Sau đó ta vào trang web và tất cả bài viết đã quay trở lại là quá trình khôi phục thành công

![Imgur](https://i.imgur.com/Zpd2Ll1.png)