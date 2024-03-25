# Sao lưu và phục hồi dự liệu trong Galera Cluster trên CentOS 7

Dưới đây là một quy trình sao lưu và phục hồi dữ liệu trên một cụm Galera Cluster triển khai trên 3 node, kết hợp với các công nghệ như HAProxy, Pacemaker và Corosync:

### Quy trình sao lưu dữ liệu:

Trước khi thực hiện sao lưu dữ liệu ta vào trang quản trị wordpress tạo ra các bài viết để nhằm mục đích kiểm tra việc backup và restore


![Imgur](https://i.imgur.com/j2hB6Re.png)



1. **Dừng ghi trên tất cả các nút (nodes)**:
   - Đảm bảo rằng không có thay đổi dữ liệu xảy ra trong quá trình sao lưu bằng cách dừng ghi trên tất cả các nút.

	```sh
	SET GLOBAL wsrep_on=OFF;
	```

2. **Thực hiện sao lưu dữ liệu**:
   - Sử dụng công cụ sao lưu như `mysqldump` hoặc các công cụ sao lưu khác để tạo bản sao lưu của dữ liệu cơ sở dữ liệu Galera Cluster.

	```sh
	mysqldump -u root -p -all-databases > 25_3_2024_backup.sql
	```


3. **Lưu trữ bản sao lưu một cách an toàn**:
   - Lưu trữ bản sao lưu ở một vị trí an toàn, có thể trên một hệ thống lưu trữ ngoài hoặc trên một máy chủ khác trong mạng.

Sau khi backup xong, ta tiến hành vào wordpress và xóa tất cả các bài viết vừa tạo đi

![Imgur](https://i.imgur.com/uImOl8p.png)



### Quy trình phục hồi dữ liệu:
1. **Phục hồi dữ liệu từ bản sao lưu**:
   - Sử dụng công cụ phục hồi dữ liệu như `mysql` để phục hồi dữ liệu từ bản sao lưu đã tạo.

	```sh
	mysql -u root -p < 25_3_2024_backup.sql
	```

4. **Kiểm tra tính toàn vẹn và khả năng truy cập**:
   - Kiểm tra xem dữ liệu đã được phục hồi đúng cách bằng cách truy cập và xem xét một số mẫu dữ liệu.
   - Đảm bảo rằng tất cả các ứng dụng và dịch vụ đang sử dụng cụm Galera Cluster có thể truy cập và sử dụng dữ liệu một cách bình thường.

   - Lúc này ta vào lại trang wordpress và thấy tất cả các bài viết đã quay trở lại là thành công


![Imgur](https://i.imgur.com/AyVgY7L.png)

5. **Tái thiết lập việc ghi trên cụm**:
   - Khi dữ liệu đã được phục hồi và cụm Galera Cluster hoạt động bình thường, tái thiết lập việc ghi trên cụm để tiếp tục hoạt động và cập nhật dữ liệu.

	```sh
	SET GLOBAL wsrep_on=ON;
	```

Quan trọng nhất là phải thực hiện kiểm tra kỹ lưỡng và thử nghiệm sau khi phục hồi để đảm bảo tính toàn vẹn và hiệu suất của cụm Galera Cluster.


![Imgur](https://i.imgur.com/IZQiyA5.png)