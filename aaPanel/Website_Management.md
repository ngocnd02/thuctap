## Quản lý website

[Custom Website default](#custom-website-default)

[Default website](#default-website)

[Website list](#website-list)

[Stop/Run/Delete of the website](#stop/run/delete-of-the-website)

[Backup Website](#backup-website)

[Multi domain management](#multi-domain-management)

[Website traffic limit](#website-traffic-limit)


### Custom Website default 

- **aaPanel >> Website >> set default page**: Ở đây bạn có thể tùy chỉnh trang web mặc định 

![Imgur](https://i.imgur.com/asTKHgJ.png)

- Trong đó: 
	- Default indexes: Trang web tạo ra một trang gợi ý được tạo mặc định.

	- 404 error page: Mã trạng thái là 404, trang gợi ý lỗi được trả về bởi máy chủ.

	- Bank page: Trang trắng của Nginx / Trang trắng của Apache: Máy chủ không thể tìm thấy trang web tương ứng, trang gợi ý lỗi được hiển thị.

	- Default site stop page: Một trang được sử dụng để phản hồi thông tin dừng trang web. Nếu không có yêu cầu liên quan, vui lòng không sửa đổi nó.

### Default website
- Sau khi thiết lập trang web mặc định, tất cả các tên miền và địa chỉ IP chưa được liên kết sẽ được chuyển hướng đến trang web mặc định. Điều này có thể ngăn chặn hiệu quả các hoạt động phân tích độc hại.

![Imgur](https://i.imgur.com/2Tw8DgU.png)

### Website list

Hiển thị danh sách trang web hiện tại, quản lý và cấu hình trang web hiện tại.

![Imgur](https://i.imgur.com/nRtJf0t.png)


- Tên trang web: Tên miền được liên kết với trang web. Nhấn vào tên trang web của trang web hiện tại để cấu hình và sửa đổi trang web hiện tại.

- Trạng thái: Hiển thị trạng thái hoạt động của trang web hiện tại. Nhấn vào trạng thái hoạt động của trang web hiện tại để tắt trang web hiện tại.

- Sao lưu: Hiển thị trạng thái sao lưu của trang web hiện tại, nhấn vào trạng thái sao lưu của trang web hiện tại để xem và sao lưu thông tin trang web hiện tại.

- Thư mục gốc: Hiển thị đường dẫn thư mục hiện tại của trang web, nhấn vào thư mục của trang web hiện tại sẽ chuyển trực tiếp đến thư mục hiện tại của quản lý tệp.

- Thời gian hết hạn: Hiển thị thời gian hiệu lực của trang web hiện tại, nhấn để đặt thời gian hết hạn của trang web hiện tại (mặc định là vô thời hạn).

### Stop/Run/Delete of the website

**Stop a website**

![Imgur](https://i.imgur.com/YEQnS62.png)

Sau khi stop, website của bạn sẽ không thể truy cập

![Imgur](https://i.imgur.com/iJwU08w.png)


**Run a website**

![Imgur](https://i.imgur.com/FfefZyV.png)

**Delete a website**
Nếu bạn chỉ muốn xóa cấu hình trang web mà không muốn xóa nội dung và cơ sở dữ liệu, hãy không chọn tùy chọn tương ứng.

![Imgur](https://i.imgur.com/aLJNRQ7.png)

### Backup Website
Manual backup

![Imgur](https://i.imgur.com/safHyc0.png)

![Imgur](https://i.imgur.com/HylMp14.png)

Automatic backup

![Imgur](https://i.imgur.com/aQdqEkK.png)

![Imgur](https://i.imgur.com/wdD5AGT.png)

### Multi domain management

Nếu bạn muốn nhiều tên miền trỏ vào một trang web cùng một lúc, hãy thiết lập nó trong quản lý tên miền.

![Imgur](https://i.imgur.com/xMnIzHJ.png)

![Imgur](https://i.imgur.com/8HN4Eb9.png)

Điền một tên miền mỗi dòng
Hỗ trợ tên miền aapanel  (.aapanel.com)
Nếu tên miền được thêm không thể truy cập được, vui lòng kiểm tra xem có giải quyết DNS không.

### Website traffic limit
Bạn có thể đặt giới hạn lưu lượng tương ứng để kiểm soát việc tiêu thụ băng thông mạng của trang web.

![Imgur](https://i.imgur.com/rBbcCUz.png)

- **Limit plan**: Bảng điều khiển cung cấp các schemes, forum / blog, picture station, download station, shopping mall, portal, enterprise station, video station. Các kế hoạch trên chỉ mang tính chất tham khảo, và các tham số dưới đây có thể được sửa đổi theo nhu cầu cá nhân;

- **Limit of concurrency**: Giới hạn số kết nối tối đa trên trang web hiện tại;

- **Sigle IP limit**: Giới hạn số lượng kết nối cùng một lúc của mỗi địa chỉ IP.

- **Trafic control**: Giới hạn ngưỡng trên lưu lượng cho mỗi yêu cầu (đơn vị: KB);

Sau khi hoàn tất sửa đổi, nhấn Lưu để hoàn tất.