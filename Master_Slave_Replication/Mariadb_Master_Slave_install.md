# Cài đặt mô hình Mater-Slave Replication với Mariadb trên Centos 7

### Bước 0: Chuẩn bị

- Ta cần 2 máy, 1 máy với vai trò làm master, và máy còn lại là slave
	- Master: 192.168.249.172

	- Slave: 192.168.249.173

- Đổi tên máy (Không cần thiết, nhưng nên đổi)

```
hostnamectl set-hostname node 1
```

- Tắt firewall

```
systemctl stop firewalld
systemctl disable firewalld
```

- Tắt selinux

```
vi /etc/selinux/config

SELINUX=disabled
```

- Cập nhật hệ thống

```
yum -y update
```

- Làm tương tự với máy slave


### Bước 1: Cài đặt MariaDB trên cả Master và Slave

1. Cài đặt MariaDB bằng lệnh sau trên cả Master và Slave:

    ```
    yum install mariadb-server mariadb
    ```

2. Khởi động dịch vụ MariaDB:

    ```
    systemctl start mariadb
    ```

3. Tùy chỉnh bảo mật MariaDB bằng cách chạy lệnh:

    ```
    mysql_secure_installation
    ```

### Bước 2: Cấu hình Master MariaDB

1. Mở tệp cấu hình MariaDB:

    ```
    vi /etc/my.cnf.d/server.cnf
    ```

2. Thêm hoặc cập nhật các cài đặt sau trong phần `[mysqld]`:

    ```
    [mysqld]
    server-id=1
    log_bin=mysql-bin
    binlog_format=row
    ```

3. Khởi động lại dịch vụ MariaDB:

    ```
    systemctl restart mariadb
    ```

### Bước 3: Cấu hình Slave MariaDB

1. Tương tự như trên, mở tệp cấu hình MariaDB trên Slave:

    ```
    vi/etc/my.cnf.d/server.cnf
    ```

2. Thêm hoặc cập nhật các cài đặt sau trong phần `[mysqld]`:

    ```
    [mysqld]
    server-id=2
    ```

3. Khởi động lại dịch vụ MariaDB:

    ```
    systemctl restart mariadb
    ```

### Bước 4: Thiết lập Replication trên Master

1. Đăng nhập vào MariaDB trên Master:

    ```
    mysql -u root -p
    ```

2. Tạo user cho replication trên Master:

    ```sql
    CREATE USER 'replication_user'@'%' IDENTIFIED BY 'password';
    GRANT REPLICATION SLAVE ON *.* TO 'replication_user'@'%';
    ```

- Trong đó: 

	- **replication_user**: là tên bạn muốn dùng để tạo một người dùng mới trong MariaDB có quyền sao chép cho một slave server

	- **password**: mật khẩu

3. Lấy thông tin về binary log file và position:

    ```sql
    SHOW MASTER STATUS;
    ```

    Ghi nhớ giá trị của `File` và `Position`.


![Imgur](https://i.imgur.com/JIrZRzZ.png)


### Bước 5: Thiết lập Replication trên Slave

1. Đăng nhập vào MariaDB trên Slave:

    ```
    sudo mysql -u root -p
    ```

2. Thiết lập Slave:

    ```sql
    CHANGE MASTER TO
    MASTER_HOST='192.168.249.172',
    MASTER_USER='ngocnd',
    MASTER_PASSWORD='password',
    MASTER_LOG_FILE='mysql_bin.000001',
    MASTER_LOG_POS=549;
    ```

![Imgur](https://i.imgur.com/1UZYQcn.png)



**Chú ý:** MASTER_LOG_FILE='mysql_bin.000001',MASTER_LOG_POS=549 2 giá trị này ta lấy ở bảng mà khi ta vừa thiết lập cho master và dùng câu lệnh **SHOW MASTER STATUS;**. Phải đúng giá trị này thì master với slave mới có thể đồng bộ

3. Khởi động Slave:

    ```sql
    START SLAVE;
    ```

4. Kiểm tra trạng thái của Slave:

    ```sql
    SHOW SLAVE STATUS\G
    ```

![Imgur](https://i.imgur.com/4cbcdPP.png)



    Đảm bảo rằng `Slave_IO_Running` và `Slave_SQL_Running` là `Yes`.

Sau khi hoàn thành, cơ sở dữ liệu Master sẽ đồng bộ dữ liệu với Slave. Đảm bảo rằng tường lửa trên cả Master và Slave cho phép kết nối từ các máy chủ khác.


### Bước 6: Kiểm tra

- Bây giờ để kiểm tra tính đồng bộ của mô hình ta vừa cài đặt, ta tạo một cơ sở dữ liệu trên master, và sau đó ta vào máy slave nếu database ta vừa tồn tại thì đã thành công. 

- Trên máy Master

![Imgur](https://i.imgur.com/RGc414p.png)


- Trên máy Slave

![Imgur](https://i.imgur.com/Tk2fdTT.png)
