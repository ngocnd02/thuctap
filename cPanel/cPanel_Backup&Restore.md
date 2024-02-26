## Backup and Restore trong cPanel

### Ful backup
- cPanel cung cấp các tùy chọn để sao lưu và khôi phục lại dữ liệu

- Trước khi tiến hành backup ta vào trang quản trị web trong wordpress tạo một số bài viết để kiểm tra tính backup và restore của cPanel

![Imgur](https://i.imgur.com/VMisjTX.png)

- Truy cập tài khoản cPanel mà bạn muốn backup
- Chọn **cPanel » Home » Files » Backup**

![Imgur](https://i.imgur.com/z3d3NiG.png)

- Nếu muốn tạo full backup ta chọn **Download a Full Account Backup**

![Imgur](https://i.imgur.com/oWChhUf.png)

![Imgur](https://i.imgur.com/tyHMqWT.png)

- Sau khi hệ thống hoàn thành file backup xong sẽ có thông báo đến email và có xuất hiện file backup 

![Imgur](https://i.imgur.com/bFr1aRY.png)

## Restore
- Trước khi tiến hành restore, ta vào trang quản trị wordpress và xóa tất cả các bài viết đi

![Imgur](https://i.imgur.com/kl42LCr.png)

- Để Restore từ file full backup, ta đăng nhập vào giao diện quản trị WHM, chọn Transfers -> Transfer or Restore a cPanel Account

![Imgur](https://i.imgur.com/zv3iYr6.png)

- Lưu ý: Khi bạn chuyển giao hoặc khôi phục một tài khoản, hãy đảm bảo rằng máy chủ của bạn có ít nhất gấp đôi kích thước tệp lưu trữ cần thiết trên không gian đĩa. Hệ thống yêu cầu có không gian đĩa trống để giải nén tệp.

- Tùy chỉnh các tùy chọn mà bạn muốn thực hiện restore

![Imgur](https://i.imgur.com/IBi91I7.png)

![Imgur](https://i.imgur.com/kYmKEK5.png)

- Trong đó:
	- **Restricted Restore**: là chức năng khiến hệ thống thực hiện thêm các kiểm tra bảo mật trên tệp tin backup. Nếu 1 phần của tệp tin có 1 vấn đề nào về bảo mật, hệ thống sẽ không thực hiện khôi phục phần đó của tệp tin lưu trữ. Lựa chọn này sẽ làm giảm những rủi ro của việc di chuyển file từ những nguồn không quen thuộc

	- **Transfer Options**: lựa chọn phương thức transfer/restore (từ local cpmove file/upload 1 cpmove file để restore/ di chuyển dữ liệu từ account cPanel từ xa)

	- **Overwrite Existing**: nếu bạn muốn overwrite account với dữ liệu ở trong backup file, hãy chọn option này

	- Cuối cùng, chọn sẽ thay thế toàn bộ địa chỉ IP của server cũ bằng địa chỉ mới hay chỉ thay thế các bản ghi A cơ bản được cung cấp bởi cPanel ở trong tệp tin zone


- Sau khi chắc chắn, chọn Restore để tiến hành khôi phục

! [Imgur](https://i.imgur.com/amUvGu6.png)

- Sau khi khôi phục thành công quay trở lại trang quản lý wordpress đã thấy tất cả các bài viết quay trở lại

![Imgur](https://i.imgur.com/5ZrWcyg.png)