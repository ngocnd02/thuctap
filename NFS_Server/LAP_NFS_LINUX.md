# Triển khai NFS server trên CentOS

Tệp hệ thống netwrok (Network File System) là một giao thức hệ thống tệp phân tán phổ biến cho phép người dùng gắn các thư mục từ xa trên máy chủ của họ. NFS cho phép bạn tận dụng không gian lưu trữ ở một vị trí khác và cho phép bạn ghi vào cùng một không gian từ nhiều máy chủ hoặc máy khách một cách dễ dàng. Do đó, nó hoạt động khá tốt đối với các thư mục mà người dùng cần truy cập thường xuyên.

## NFS server
- Đầu tiên, chúng ta sẽ cài đặt dịch vụ NFS trên CentOS server với yum: 
```yum -y install nfs-utils```

- Bây giờ tạo một thư mục sẽ được chia sẻ bởi NFS
```mkdir /nfsshare```

- Tiếp theo chúng ta cần khởi động các dịch vụ và cho phép chúng khởi động khi khởi động 
```
systemctl enable rpcbind
systemctl enable nfs-server
systemctl enable nfs-lock
systemctl enable nfs-idmap
systemctl start rpcbind
systemctl start nfs-server
systemctl start nfs-lock
systemctl start nfs-idmap
```
Trong đó: 
	- **rpcbind**: Là một dịch vụ cung cấp thông tin cấu hình và kết nối cho các dịch vụ sử dụng RPC (Remote Procedure Call).

	- **nfs-server**: Dịch vụ NFS chính, cung cấp khả năng chia sẻ tệp tin và thư mục qua mạng.

	- **nfs-lock**: Dịch vụ quản lý khóa cho NFS, đảm bảo đồng bộ hóa truy cập tệp tin giữa các máy chủ và người dùng.

	- **nfs-idmap**: Dịch vụ quản lý ánh xạ ID giữa các hệ thống, giúp giải quyết vấn đề đồng bộ hóa quản lý người dùng và nhóm người dùng trên các máy chủ.

- Bây giờ, chúng ta sẽ chia sẻ thư mục NFS qua mạng:
```vi /etc/exports```

- Chúng ta sẽ tạo điểm chia sẻ /nfsshare. Hãy chỉnh sửa file exprots như sau: 

![Imgur](https://i.imgur.com/XQb1PJC.png)

Trong đó: 
	- **nfsshare**: Đường dẫn đến thư mục hoặc tệp tin mà bạn muốn chia sẻ qua NFS.

	- **192.168.249.153**: Địa chỉ IP của máy client được phép truy cập dịch vụ NFS.

	- **rw**: Cho phép quyền đọc và ghi (read-write).

	- **sync**: Đảm bảo dữ liệu được đồng bộ hóa trước khi phản hồi ghi được trả về.

	- **no_root_squash**: Cho phép quyền root trên client thực hiện các thao tác như root trên máy chủ (không squash).

	- **no_all_squash**: Cho phép tất cả người dùng trên client giữ nguyên quyền truy cập của họ mà không bị squash (giảm quyền).

**NOTE**: 192.168.249.153 là địa IP của máy khách (client). Nếu bạn muốn cho phép bất kỳ máy khách nào khác truy cập, bạn cần thêm địa chỉ IP của chúng; nếu không, bạn có thể thêm "*" thay vì địa chỉ IP để cho phép truy cập từ mọi địa chỉ IP.
Điều kiện là cả hai đầu (máy chủ và máy khách) đều có thể truy cập được thông qua ping. 

- Cuối cùng, khởi động lại dịch vụ NFS:
```systemctl restart nfs-server```

- Nếu tường lửa của bạn bật, chúng ta phải thêm dịch vụ NFS vào tường lửa để cho phép sử dụng dịch vụ nfs.
```sh
firewall-cmd --permanent --zone=public --add-service=nfs
firewall-cmd --permanent --zone=public --add-service=mountd
firewall-cmd --permanent --zone=public --add-service=rpc-bind
firewall-cmd --reload
```
# Triển khai NFS Client là CentOS
- Trong máy CentOS, trước tiên ta cũng phải cài dịch vụ NFS:
```yum install nfs-utils```

- Tiếp theo ta tạo các điểm gắn kết (mount points) cho thư mục NFS. 
```
mkdir /nfs
```
- Tiếp theo, Chúng ta sẽ gắn kết thư mục chia sẻ của NFS vào thư mục nfsshare trên máy khách như dưới đây:
```
mount -t nfs 192.168.249.154:/nfsshare /nfs
```
- Nó sẽ mount /nfsshare của NFS server.
- Sử dụng lệnh **df-hT** để kiểm tra xem đã mount thành công hay chưa. 

![Imgur](https://i.imgur.com/1RuDXbp.png)

- Lúc này 2 máy đã có thể chia sẻ tệp tin hoặc thư mục cho nhau. 
- Ở trên máy NFS server ta đã tạo ra một file intro.txt trong /nfsshare. và bây giờ sau khi chia sẻ nfs với client. Ta mở thư mục /nfs đã thấy có file intro.txt nghĩa là 2 máy đã có thể chia sẻ tệp tin và thư mục cho nhau.

**NOTE**: Lệnh mount trong Centos sẽ bị mất khi chúng ta reboot lại hệ thống, nên chúng ta phải cấu hình sao cho không bị mất ngay cả khi reboot. 
- Để cấu hình, ta vào /etc/fstab để cấu hình như sau: 
```
192.168.249.154:/nfsshare /nfs nfs defaults 0 0
```
Trong đó: 
	- 192.168.249.154:/nfsshare: Là địa chỉ IP của máy chủ NFS và đường dẫn đến thư mục chia sẻ trên máy chủ.

	- /nfs: Là đường dẫn đến thư mục trên máy khách để gắn kết thư mục NFS.

	- nfs: Là loại hệ thống tệp tin.

	- defaults: Là tùy chọn mặc định cho mount point.

	- 0 0: Là các tham số để xác định thứ tự kiểm tra và sao lưu. (Thường để mặc định).

![Imgur](https://i.imgur.com/NtmJROL.png)
