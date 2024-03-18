# Cài đặt Galera 3 node trên Centos 7

## Tổng quan
MariaDB là một sản phẩm mã đóng tách ra từ mã mở do cộng đồng phát triển của hệ quản trị cơ sở dữ liệu quan hệ MySQL nhằm theo hướng không phải trả phí với GNU GPL. MariaDB được phát triển từ sự dẫn dắt của những nhà phát triển ban đầu của MySQL, do lo ngại khi MySQL bị Oracle Corporation mua lại. Những người đóng góp được yêu cầu chia sẽ quyền tác giả của họ với MariaDB Foundation.

MariaDB được định hướng để duy trì khả năng tương thích cao với MySQL, để đảm bảo khả năng hỗ trợ về thư viện đồng thời kết hợp một cách tốt nhất với các API và câu lệnh của MySQL. MariaDB đã có công cụ hỗ lưu trữ XtraDB thay cho InnoDB.

MariaDB Galera Cluster là giải pháp sao chép đồng bộ nâng cao tính sẵn sàng cho MariaDB. Galera hỗ trợ chế độ Active-Active tức có thể truy cập, ghi dữ liệu đồng thời trên tất các node MariaDB thuộc Galera Cluster.

## Chuẩn bị
Server có cấu hình như sau: 


![Imgur](https://i.imgur.com/TZPJQbT.png)

## Thiết lập ban đầu 
### Tại node1
- Cấu hình hostname

```
hostnamectl set-hostname node1
```

- Tắt firewall, selinux, và khởi động lại hệ thống

```
systemctl stop firewalld
systemctl disabled firewalld
```

```
vi /etc/selinux/config

SELINUX=disabled
```

```
reboot
```

- Cấu hình host

```
192.168.249.170 node1
192.168.249.171 node2
```

### Tại node 2

- Cấu hình hostname

```
hostnamectl set-hostname node2
```

- Tắt firewall, selinux, và khởi động lại hệ thống

```
systemctl stop firewalld
systemctl disabled firewalld
```

```
vi /etc/selinux/config

SELINUX=disabled
```

```
reboot
```

- Cấu hình host

```
192.168.249.170 node1
192.168.249.171 node2
```

## Cài đặt Mariadb 10.5
**Thực hiện trên tất cả node1 và node2**
- MariaDB có thể được cài đặt từ trình quản lý gói yum của CentOS. Bạn cần thêm repository MariaDB vào hệ thống của mình trước khi cài đặt. Tạo một tệp repo mới bằng lệnh sau:

```
vi /etc/yum.repos.d/MariaDB.repo
```
- Sau đó thêm dòng sau vào tệp

```
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.5/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

- Cài đặt thêm gói epel-release

```
yum install -y epel-release
```

- Cập nhật hệ thống trước khi cài đặt mariadb

```
yum -y update
```

- Cài đặt Mariadb

```
yum install MariaDB-server MariaDB-client
```

![Imgur](https://i.imgur.com/yb4RUyk.png)


- Cài đặt các gói Galera và các gói hỗ trợ

```
yum install -y galera rsync
```

![Imgur](https://i.imgur.com/n6OYBqD.png)

- Tắt MariaDB (do liên quan tới cấu hình Galera MariaDB)

```
systemctl stop mariadb
```

## Phần 3. Cấu hình Galera Cluster
### Tại node 1
- Sao chép  tệp cấu hình server.cnf từ thư mục /etc/my.cnf.d/ và lưu trữ bản sao dự phòng dưới tên server.cnf.bak cũng trong thư mục đó (/etc/my.cnf.d/). Điều này giúp đảm bảo rằng bạn có một bản sao của tệp cấu hình gốc trước khi thực hiện bất kỳ thay đổi nào. 

```
cp /etc/my.cnf.d/server.cnf /etc/my.cnf.d/server.cnf.bak
```

- Sau đó chỉnh sửa cấu hình trong file **server.cnf**

```
echo '[server]
[mysqld]
bind-address=192.168.249.170

[galera]
wsrep_on=ON
wsrep_provider=/usr/lib64/galera/libgalera_smm.so
#add your node private ips here
wsrep_cluster_address="gcomm://192.168.249.170,192.168.249.171"
binlog_format=row
default_storage_engine=InnoDB
innodb_autoinc_lock_mode=2
#Cluster name
wsrep_cluster_name="portal_cluster"
# Allow server to accept connections on all interfaces.
bind-address=192.168.249.170
# this server private ip, change for each server
wsrep_node_address="192.168.249.170"
# this server name, change for each server
wsrep_node_name="node1"
wsrep_sst_method=rsync
[embedded]
[mariadb]
[mariadb-10.2]
' > /etc/my.cnf.d/server.cnf


**Lưu ý:**
- **wsrep_cluster_address**: Danh sách các node thuộc Cluster, sử dụng địa chỉ IP (Trong bài lab này là 192.168.249.170, 192.168.249.171)

- **wsrep_cluster_name:** Tên của cluster

- **wsrep_node_address:** Địa chỉ IP của node đang thực hiện

- **wsrep_node_name:** Tên node (Giống với hostname)

- **Không được bật mariadb (Quan trọng, nếu không sẽ dẫn tới lỗi khi khởi tạo Cluster)**

![Imgur](https://i.imgur.com/hxE2plc.png)


### Tại node2

```
cp /etc/my.cnf.d/server.cnf /etc/my.cnf.d/server.cnf.bak
```

- Sau đó chỉnh sửa cấu hình trong file **server.cnf**

```
echo '[server]
[mysqld]
bind-address=192.168.249.171

[galera]
wsrep_on=ON
wsrep_provider=/usr/lib64/galera/libgalera_smm.so
#add your node private ips here
wsrep_cluster_address="gcomm://192.168.249.170,192.168.249.171"
binlog_format=row
default_storage_engine=InnoDB
innodb_autoinc_lock_mode=2
#Cluster name
wsrep_cluster_name="portal_cluster"
# Allow server to accept connections on all interfaces.
bind-address=192.168.249.171
# this server private ip, change for each server
wsrep_node_address="192.168.249.171"
# this server name, change for each server
wsrep_node_name="node2"
wsrep_sst_method=rsync
[embedded]
[mariadb]
[mariadb-10.2]
' > /etc/my.cnf.d/server.cnf


## Khởi động dịch vụ
- Tại **node 1** khởi tạo Cluster

```
galera_new_cluster

```
- Khởi động lại dịch vụ Mariadb

```
systemctl start mariadb
systemctl enable mariadb
```

**Lưu ý:**Từ bản Mariadb 10.4 trở lên thì phải tạo symlink như sau rồi mới khởi tạo cluster: 

```
ln -s /usr/lib64/galera-4 /usr/lib64/galera
```

- Tại 2 node còn lại chạy dịch vụ mariadb (nếu sử dụng Mariadb 10.4 trở lên thì cũng phải tạo symlink như trên)

```
systemctl start mariadb
systemctl enable mariadb
```

## Kiểm tra tại node1
```
mysql -u root -e "SHOW STATUS LIKE 'wsrep_cluster_size
```

![Imgur](https://i.imgur.com/IJ4GpuY.png)


# Triển khai Haproxy Pacemaker cho Cluster Galera 3 node trên CentOS 7
## Cài đặt Haproxy bản 1.8
**Thực hiện trên tất cả các node**
- Cài đặt wget và socat từ kho lưu trữ của CentOS. 

```
yum install wget socat -y
```

- Tải xuống gói RPM của HAProxy phiên bản 1.8.1 từ URL được cung cấp.

```
wget http://cbs.centos.org/kojifiles/packages/haproxy/1.8.1/5.el7/x86_64/haproxy18-1.8.1-5.el7.x86_64.rpm
```

- Cài đặt gói RPM HAProxy vừa tải xuống. 

```
yum install haproxy18-1.8.1-5.el7.x86_64.rpm -y
```

- Tạo bản backup cho cấu hình mặc định và chỉnh sửa cấu hình HAproxy

```
cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.bak
```

- Cầu hình Haproxy

```
echo 'global
    log         127.0.0.1 local2
    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     4000
    user        haproxy
    group       haproxy
    daemon
    stats socket /var/lib/haproxy/stats
defaults
    mode                    http
    log                     global
    option                  httplog
    option                  dontlognull
    option http-server-close
    option forwardfor       except 127.0.0.0/8
    option                  redispatch
    retries                 3
    timeout http-request    10s
    timeout queue           1m
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    timeout http-keep-alive 10s
    timeout check           10s
    maxconn                 3000

listen stats
    bind :8080
    mode http
    stats enable
    stats uri /stats
    stats realm HAProxy\ Statistics

listen galera
    bind 192.168.249.175:3306
    balance source
    mode tcp
    option tcpka
    option tcplog
    option clitcpka
    option srvtcpka
    timeout client 28801s
    timeout server 28801s
    option mysql-check user haproxy
    server node1 192.168.249.170:3306 check inter 5s fastinter 2s rise 3 fall 3
    server node2 192.168.249.171:3306 check inter 5s fastinter 2s rise 3 fall 3 backup' > /etc/haproxy/haproxy.cfg
```

- Cấu hình Log cho HAProxy

```
sed -i "s/#\$ModLoad imudp/\$ModLoad imudp/g" /etc/rsyslog.conf
sed -i "s/#\$UDPServerRun 514/\$UDPServerRun 514/g" /etc/rsyslog.conf
echo '$UDPServerAddress 127.0.0.1' >> /etc/rsyslog.conf

echo 'local2.*    /var/log/haproxy.log' > /etc/rsyslog.d/haproxy.conf

systemctl restart rsyslog
```

- Bổ sung cấu hình cho phép kernel có thể binding tới IP VIP

```
echo 'net.ipv4.ip_nonlocal_bind = 1' >> /etc/sysctl.conf
```

- Tắt dịch vụ HAProxy

```
systemctl stop haproxy
systemctl disable haproxy
```

- Tạo user haproxy, phục vụ plugin health check của HAProxy 

Đăng nhập vào MySQL hoặc MariaDB:

```
mysql -u root -p
```

- Sau đó, nhập mật khẩu cho tài khoản quản trị để đăng nhập.

- Tạo người dùng và cấp quyền truy cập:

```
CREATE USER 'haproxy'@'node1';
CREATE USER 'haproxy'@'node2';
CREATE USER 'haproxy'@'%';
```

- Cấp quyền truy cập cho người dùng:

```
GRANT ALL PRIVILEGES ON *.* TO 'haproxy'@'node1';
GRANT ALL PRIVILEGES ON *.* TO 'haproxy'@'node2';
GRANT ALL PRIVILEGES ON *.* TO 'haproxy'@'%';
```

## Triển khai Cluster Pacemaker

### Bước 1: Cài đặt pacemaker corosync
**Lưu ý: Thực hiện trên tất cả các node**

- Cài đặt gói pacemaker pcs

```
yum -y install pacemaker pcs

systemctl start pcsd 
systemctl enable pcsd
```

- Thiết lập mật khẩu user hacluster

```
passwd hacluster
```

![Imgur](https://i.imgur.com/o3gKtou.png)

- Lưu ý: Nhập chính xác và nhớ mật khẩu user hacluster, đồng bộ mật khẩu trên tất cả các node

### Bước 2: Tạo Cluster
Chứng thực cluster (Chỉ thực thiện trên cấu hình trên một node duy nhất, trong bài sẽ thực hiện trên **node1**), nhập chính xác tài khoản user hacluster

```
pcs cluster auth node1 node2

Username: hacluster
Password: *********
```

Kết quả

![Imgur](https://i.imgur.com/Z4xJZ7c.png)


- Khởi tạo cấu hình cluster ban đầu

```
pcs cluster setup --name ha_cluster node1 node2
```

Kết quả

![Imgur](https://i.imgur.com/J63qt8p.png)

-Lưu ý:

	- ha_cluster: Tên của cluster khởi tạo

	- node01, node02, node03: Hostname các node thuộc cluster, yêu cầu khai báo trong /etc/host


- Khởi động Cluster

```
pcs cluster start --all
```

- Cho phép khởi động cùng OS

```
pcs cluster enable --all
```

Kết quả

![Imgur](https://i.imgur.com/vVw1MXg.png)


### Thiết lập Cluster

**Bỏ qua cơ chế STONITH**

```
pcs property set stonith-enabled=false
```
- Đây là cấu hình để vô hiệu hóa tính năng STONITH (Shoot The Other Node In The Head) trong cụm Pacemaker. STONITH là một cơ chế an toàn để đảm bảo không xảy ra sự đối chọi (split-brain) trong một cụm hoạt động. 


**Cho phép Cluster chạy kể cả khi mất quorum**

```
pcs property set no-quorum-policy=ignore
```

- Đây là cấu hình chính sách "no-quorum" trong cụm Pacemaker. Chính sách này xác định cách hành xử của hệ thống khi không đạt được quorum, tức là khi không đủ số lượng node hoạt động trong cụm để đảm bảo tính toàn vẹn của cụm. Trong trường hợp này, chính sách được thiết lập là "ignore", có nghĩa là Pacemaker sẽ tiếp tục hoạt động ngay cả khi không đạt được quorum. Thường thì, việc thiết lập chính sách này thành "ignore" chỉ thích hợp trong các trường hợp đặc biệt và cần được xem xét kỹ lưỡng, vì có thể dẫn đến tình trạng split-brain và mất tính toàn vẹn dữ liệu.


**Hạn chế Resource trong cluster chuyển node sau khi Cluster khởi động lại**

```
pcs property set default-resource-stickiness="INFINITY"
```
- Khi đặt độ ưu tiên của một tài nguyên thành "INFINITY", nó có nghĩa là tài nguyên đó sẽ không bao giờ được chuyển đi sang một node khác nếu node hiện tại đang chứa tài nguyên đó vẫn hoạt động. Điều này giúp đảm bảo tính ổn định của các dịch vụ hoặc ứng dụng được triển khai trên cụm Pacemaker, bằng cách đảm bảo rằng các tài nguyên quan trọng sẽ ở lại trên các node đã được xác định, tránh tình trạng di chuyển không cần thiết của chúng.


**Kiểm tra thiết lập cluster**

```pcs property list```

![Imgur](https://i.imgur.com/1tBzm4h.png)


**Tạo resource IP VIP Cluster**

```pcs resource create Virtual_IP ocf:heartbeat:IPaddr2 ip=192.168.249.175 cidr_netmask=24 op monitor interval=30s```

- Khi được thực hiện, tài nguyên Virtual_IP sẽ được tạo trong cụm Pacemaker, cho phép nó quản lý địa chỉ IP 192.168.249.175 và kiểm tra trạng thái của nó theo chu kỳ 30 giây.


**Tạo resource quản trị dịch vụ HAProxy*

```pcs resource create Loadbalancer_HaProxy systemd:haproxy op monitor timeout="5s" interval="5s"```
- Khi được thực hiện, tài nguyên Loadbalancer_HaProxy sẽ được tạo trong cụm Pacemaker, cho phép nó quản lý dịch vụ HAProxy dựa trên systemd và kiểm tra trạng thái của nó theo chu kỳ 5 giây.


**Ràng buộc thứ tự khởi động dịch vụ: khởi động dịch vụ Virtual_IP sau đó khởi động dịch vụ Loadbalancer_HaProxy**

```pcs constraint order start Virtual_IP then Loadbalancer_HaProxy kind=Optional```

**Ràng buộc resource Virtual_IP phải khởi động cùng node với resource Loadbalancer_HaProxy**

```
pcs constraint colocation add Virtual_IP Loadbalancer_HaProxy INFINITY
```


**Kiểm tra trạng thái Cluster**

```pcs status```

![Imgur](https://i.imgur.com/OCkcwGW.png)


**Kiểm tra cấu hình Resource**

```pcs resource show --full```


![Imgur](https://i.imgur.com/eVoUzpa.png)


**Kiểm tra ràng buộc trên resource**


```
pcs constraint
```

### Phần 4: Kiểm tra
**Kiểm tra trạng thái dịch vụ**
- Truy cập <IP_VIP>:8080/stats (http://192.168.249.175:8080/stats)


![Imgur](https://i.imgur.com/vgHyPUZ.png)




