# Cài đặt NFS Server trên Windows Server 2022

## Cài đặt vai trò máy chủ NFS
- Trong windows server vào phần server manager, chọn **Add Roles and Features**

![Imgur](https://i.imgur.com/QFWQ2a1.png)

- Tiếp tục chọn next để cài đặt, trong phần **File and Storage Services** tích chọn cài đặt dịch vụ **Server for NFS**. Bằng cách chọn tùy chọn “Server for NFS”, một cửa sổ bật lên sẽ xuất hiện yêu cầu bạn thêm và xác nhận các tính năng cần thiết cho máy chủ cho NFS; vì mục đích này, hãy nhấp vào “Add features” > “Next”.

![Imgur](https://i.imgur.com/OjoG33N.png)

- Cuối cùng nhấn **Install** để cài đặt 

![Imgur](https://i.imgur.com/VFsSqGM.png)


## Thiết lập một thư mục chia sẻ
- Trong ổ C hoặc bất kì ổ nào đó bạn thích, tạo một thư mục mới. Ở đây ta tạo một thư mục có tên là NFS_SHARE dùng để chia sẻ cho các máy client. 

- Vào lại **server manager** chọn **File and Storage Services**

![Imgur](https://i.imgur.com/tlJxcNS.png)

- Bấm chọn **Shares**

![Imgur](https://i.imgur.com/J6ecaDs.png)

- Trong phần task hoặc kích chuột phải chọn **New share**. Sau khi hiển thị lên cửa sổ mới chọn **NFS Share-Quick** 

![Imgur](https://i.imgur.com/UPctrn2.png)

- Trong mục **Share Location** chọn tùy chọn “Type a custom path” cho vị trí chia sẻ của bạn và chọn thư mục và thư mục mong muốn cho chia sẻ NFS mà bạn muốn tạo thông qua nút “Browse”. Bạn cũng có thể nhập đường dẫn đầy đủ của thư mục và nhấp vào “Next”.

![Imgur](https://i.imgur.com/MWG2Z9f.png)

- Chọn thư mục **NFS_SHARE** mà ta vừa tạo ở trên kia

![Imgur](https://i.imgur.com/JsyIvFm.png)

- Sau khi thêm đường dẫn vào xong chọn **Next**

![Imgur](https://i.imgur.com/CMOw1x4.png)

- Trong phần **Share Name** chỉ định tên cụ thể cho chia sẻ NFS của bạn và hoàn thành các bước tạo chia sẻ NFS bằng cách chọn nút “Next”.

![Imgur](https://i.imgur.com/7UR2Ge8.png)

- Trong phần “Authentication”, bạn sẽ xác định phương thức xác thực cho chia sẻ NFS. Chọn phương pháp phù hợp với mục tiêu và nhu cầu của bạn. Bằng cách chọn tất cả các tùy chọn Kerberos, chỉ định xác thực Kerberos mà máy chủ hỗ trợ cho máy khách. Trong phần “no server authentication”, đánh dấu các mục sau để cho phép các máy khách không có Kerberos truy cập vào chia sẻ NFS:

	- No server authentication (AUTH_SYS) (Không có xác thực máy chủ (AUTH_SYS))
	- Enable unmapped user access (Cho phép quyền truy cập của người dùng chưa được ánh xạ)
	- Allow unmapped user access by UID/GID (Cho phép người dùng chưa được ánh xạ truy cập bằng UID/GID)

![Imgur](https://i.imgur.com/ZBvulSu.png)

## Share permission
- Trong phần **Share Permissions** nhập địa chỉ của máy clinet mà bạn muốn chia sẻ, và cấp quyền Read/Wirte cho client. 

![Imgur](https://i.imgur.com/nLu9y4H.png)

![Imgur](https://i.imgur.com/Ovvw1ad.png)

- Tiếp theo trong phần Permission nếu bạn không muốn thiết lập gì thêm thì chọn **Next** để tiếp tục

![Imgur](https://i.imgur.com/s07OjST.png)

- Cuối cùng ấn **Create** để hoàn thành

![Imgur](https://i.imgur.com/p4Lbpf5.png)


## Gắn điểm chia sẻ file
- Ta có thể dùng máy client là Windows hoặc Linux để nhận file chia sẻ đều được. Ở đây ta sử dụng máy windows. 
- Trong Command Line của windows, tạo điểm mount để liên kết tới NFS server

```mount 192.168.249.164:/NFS_SHARE F:\```

- Trong đó:
	- 192.168.249.164 là địa chỉ của máy chủ NFS 
	- /NFS_SHARE là thư mục mà máy chủ NFS muốn chia sẻ
	- F là ổ đĩa bạn muốn gắn vào máy clinet

![Imgur](https://i.imgur.com/XWYlx0N.png)

- Sau khi thành công ta vào This PC và đã thấy 1 ổ F xuất hiện

![Imgur](https://i.imgur.com/nezI1mM.png)

- Mở vào ổ F, ta đã thấy 1 tệp tin ta đã tạo ở máy chủ đã có là thành công

![Imgur](https://i.imgur.com/7v58tfj.png)
