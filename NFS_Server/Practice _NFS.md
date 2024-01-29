# Triển khai NFS-Server
- Ở bài lab trước ta đã tiến hành triển khai nfs-server, có thể lại tại [đây](https://github.com/ngocnd02/thuctap/blob/main/NFS_Server/LAP_NFS_LINUX.md)

- **Đặt vấn đề**: Hiện tại trên máy nfs-server bạn có một ổ sdd với dung lượng là 10G, bây giờ bạn muốn dùng nfs để chia sẻ thư mục cho 2 máy client, máy client01 với dung lượng là 2G và máy client02 với dung lượng là 8G. 

### Triển khai trên NFS Server
- Ta tiến hành tạo lvm để có thể phân chia ổ sdd.

- Tạo Physical Volume

```pvcreate /dev/sdd```

![Imgur](https://i.imgur.com/1pwhgq7.png)

- Tạo Volume Group:

```vgcreate myvg /dev/sdd```

![Imgur](https://i.imgur.com/8aBm4cz.png)

- Tạo Logical Volume: Ta tiến hành tạo 2 LV, 1 cái có dung lượng 2G và 1 cái có dung lượng 8G

```lvcreate -n mylv1 -L 2G myvg```

```lvcreate -n mylv2 -L 8G myvg```

![Imgur](https://i.imgur.com/JQIKNYs.png)

- Tiếp theo để có thể sử dụng được 2 phân vùng ta vừa tạo, ta phải định dạng tệp tin 

```mkfs.ext4 /dev/myvg/mylv1```

```mkfs.ext4 /dev/myvg/mylv2```

- Sau đó, ta tạo 2 thư mục để chứa lần lượt 2 phân vùng ta vừa tạo ra, đó cũng chính thư mục mà ta sẽ chia sẻ với các máy client. 

```mkdir /nfs01```

```mkdir /nfs02```

- Cuối cùng tiến hành mount 2 phân vùng vào 2 thư mục vừa tạo. 

```mount /dev/myvg/mylv1 /nfs01```

```mount /dev/myvg/mylv2/nfs02```

Dùng lệnh df-h để kiểm tra: 

![Imgur](https://i.imgur.com/MSNPBhl.png)

- Tiến hành ghi lệnh mount vào thư mục /etc/fstab để khi reboot lại hệ thống không bị mất mount

```
mount /dev/myvg/mylv1 /nfs01 ext4 defaults 0 0
mount /dev/myvg/mylv2 /nfs02 ext4 defaults 0 0
```
![Imgur](https://i.imgur.com/SbUqM9P.png)


- Và bây giờ để có thể chia sẻ 2 thư mục /nfs01 và /nfs02 cho các máy client thì ta phải cấu hình trong file /etc/exports

```
/nfs01 192.168.249.161(rw,sync,no_root_squash,no_all_squash)
/nfs02 192.168.249.163(rw,sync,no_root_squash,no_all_squash)
```

![Imgur](https://i.imgur.com/10YdgrD.png)

- Sử dụng lệnh lsblk để hiện thị các phân vùng và dung lượng của phân vùng mà ta vừa tạo để chia sẻ

![Imgur](https://i.imgur.com/l2KPRcv.png)

Trong đó:
	- /nfs01 có dung lượng là 2G, ta sẽ chia sẻ cho máy client 192.168.249.161
	- /nfs02 có dung lượng là 8G, ta sẽ chia sẻ cho máy client 192.168.249.163

- Tiến hành tạo các file trong /nfs01 và /nfs02 để kiểm tra xem có chia sẻ file thành công không.

```mkdir nfs01.txt```

```mkdir nfs02.txt```

### Trên máy client 192.168.249.161
- Tạo một thư mục để xem các tệp tin được chia sẻ

```mkdir /exam01```

- Tiến hành mount để có thể nhận chia sẻ từ máy server

```mount -t nfs 192.168.249.162:/nfs01 /exam01```

- Sử dụng lệnh df-h để kiểm tra xem đã mount thành công hay chưa

![Imgur](https://i.imgur.com/rmtDDbM.png)

- Mở thư mục /exam01 lên và thấy có file nfs01.txt mà ta đã tạo ở nfs-server --> chia sẻ file thành công

![Imgur](https://i.imgur.com/XSnXanv.png)

- Tuy nhiên, để lệnh mount không bị mất khi reboot ta phải tiến hành cấu hình trong file /etc/fstab

![Imgur](https://i.imgur.com/rJjNJtD.png)


### Trên máy client 192.168.249.163
Tiến hành tương tự như máy client 161

- Tạo một thư mục để xem các tệp tin được chia sẻ

```mkdir /exam02```

- Tiến hành mount để có thể nhận chia sẻ từ máy server

```mount -t nfs 192.168.249.162:/nfs02 /exam02```

- Sử dụng lệnh df-h để kiểm tra xem đã mount thành công hay chưa

![Imgur](https://i.imgur.com/iUKCXrS.png)

- Mở thư mục /exam01 lên và thấy có file nfs02.txt mà ta đã tạo ở nfs-server --> chia sẻ file thành công

![Imgur](https://i.imgur.com/tpVE9HD.png)

- Tuy nhiên, để lệnh mount không bị mất khi reboot ta phải tiến hành cấu hình trong file /etc/fstab

![Imgur](https://i.imgur.com/r85TD4n.png)

