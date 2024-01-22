# Triển khai NFS server trên CentOS

Tệp hệ thống netwrok (Network File System) là một giao thức hệ thống tệp phân tán phổ biến cho phép người dùng gắn các thư mục từ xa trên máy chủ của họ. NFS cho phép bạn tận dụng không gian lưu trữ ở một vị trí khác và cho phép bạn ghi vào cùng một không gian từ nhiều máy chủ hoặc máy khách một cách dễ dàng. Do đó, nó hoạt động khá tốt đối với các thư mục mà người dùng cần truy cập thường xuyên.

## NFS server
- Đầu tiên, chúng ta sẽ cài đặt dịch vụ NFS trên CentOS server với yum: 
```yum -y install nfs-utils```

- Bây giờ tạo một thư mục sẽ được chia sẻ bởi NFS
```mkdir /var/nfsshare```

- Thay đổi quyền của folder như sau: 
```
chmod -R 755 /var/nfsshare
chown nfsnobody:nfsnobody /var/nfsshare
```
Chúng ta sử dụng /var/nfsshare làm thư mục dùng chung, nếu chúng ta sử dụng một ổ đĩa khác chẳng hạn như thư mục /home thì những thay đổi về quyền sẽ gây ra vấn đề lớn về quyền và phá hỏng toàn bộ hệ thống phân cấp. Vì vậy trong trường hợp chúng ta muốn chia sẻ thư mục /home thì quyền không được thay đổi.

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

- Chúng ta sẽ tạo 2 điểm chia sẻ /home và /var/nfsshare. Hãy chỉnh sửa file exprots như sau: 

![Imgur](https://i.imgur.com/mEdolMZ.png)

Trong đó: 
	- **/var/nfsshare**: Đường dẫn đến thư mục hoặc tệp tin mà bạn muốn chia sẻ qua NFS.
	- **192.168.249.135**: Địa chỉ IP của máy client được phép truy cập dịch vụ NFS.
	- **rw**: Cho phép quyền đọc và ghi (read-write).
	- **sync**: Đảm bảo dữ liệu được đồng bộ hóa trước khi phản hồi ghi được trả về.
	- **no_root_squash**: Cho phép quyền root trên client thực hiện các thao tác như root trên máy chủ (không squash).
	- **no_all_squash**: Cho phép tất cả người dùng trên client giữ nguyên quyền truy cập của họ mà không bị squash (giảm quyền).

**NOTE**: 192.168.249.135 là địa IP của máy khách (client). Nếu bạn muốn cho phép bất kỳ máy khách nào khác truy cập, bạn cần thêm địa chỉ IP của chúng; nếu không, bạn có thể thêm "*" thay vì địa chỉ IP để cho phép truy cập từ mọi địa chỉ IP.
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

## NFS Client
### Máy client là Windows
- Trong máy windows, đầu tiên chúng ta vào phần *control panel* và chọn vào **Turn Windows features on or off**

![Imgur](https://i.imgur.com/UEHgHGd.png)

- Lựa chọn vào phần **Service for NFS** và tích chọn 2 dịch vụ **Administrative Tools** và **Client for NFS**

![Imgur](https://i.imgur.com/2s6VUup.png)

- Mở cmd, sau đó gõ lệnh sau để có thể truy cập vào file được chia sẻ bởi NFS server:
```mount 192.168.249.134:/var/nfsshare F:\```

![Imgur](https://i.imgur.com/l3WNiLk.png)

- Lúc này mở this PC ta sẽ thấy thư mục được chia sẻ nằm trong ổ mà ta đã chọn 

![Imgur](https://i.imgur.com/txjAKXz.png)


### Máy client là CentOS
- Trong máy CentOS, trước tiên ta cũng phải cài dịch vụ NFS:
```yum install nfs-utils```

- Tiếp theo ta tạo các điểm gắn kết (mount points) cho thư mục NFS. 
```
mkdir -p /mnt/nfs/home
mkdir -p /mnt/nfs/var/nfsshare
```
- Tiếp theo, Chúng ta sẽ gắn kết thư mục chia sẻ của NFS vào thư mục home trên máy khách như dưới đây:
```
mount -t nfs 192.168.249.134:/home /mnt/nfs/home/
```
- Nó sẽ mount /home của NFS server. Kế tiếp, chúng ta sẽ mount thư mục /var/nfsshare
```mount -t nfs 192.168.249.134:/var/nfsshare /mnt/nfs/var/nfsshare/```

- Sử dụng lệnh *df-hT** để kiểm tra xem đã mount thành công hay chưa. 
- Lúc này 2 máy đã có thể chia sẻ tệp tin hoặc thư mục cho nhau. 

**NOTE**: Lệnh mount trong Centos sẽ bị mất khi chúng ta reboot lại hệ thống, nên chúng ta phải cấu hình sao cho không bị mất ngay cả khi reboot. 
- Để cấu hình, ta vào /etc/fstab để cấu hình như sau: 
```
192.168.249.134:/home /mnt/nfs/home nfs defaults 0 0
192.168.249.134:/var/nfsshare /mnt/nfs/var/nfsshare nfs defaults 0 0
```
Trong đó: 
	- 192.168.249.134:/var/nfsshare: Là địa chỉ IP của máy chủ NFS và đường dẫn đến thư mục chia sẻ trên máy chủ.
	- /mnt/nfs/var/nfsshare/: Là đường dẫn đến thư mục trên máy khách để gắn kết thư mục NFS.
	- nfs: Là loại hệ thống tệp tin.
	- defaults: Là tùy chọn mặc định cho mount point.
	- 0 0: Là các tham số để xác định thứ tự kiểm tra và sao lưu. (Thường để mặc định).