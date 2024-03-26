# Cấu hình thêm một node vào trong Galera Cluster

Lưu ý: trước khi ta thực hiện thêm 1 node mới, để đảm bảo sự cố ngoài ý muốn xảy ra ta nên backup cơ sở dữ liệu trước khi thực hiện join thêm 1 node để tránh mất dữ liệu. 

## Thiết lập ban đầu cho node mới muốn thêm vào
Tại node mới muốn thêm vào (Ở đây ta muốn thêm vào node thứ 4)

- Cấu hình hostname

```
hostnamectl set-hostname node4
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
192.168.249.165 node3
192.168.249.173 node4
```

- **Lưu ý: Trên các node đang tồn tại trên cụm cluster ta cũng cần phải thêm cấu hình host của node mới được thêm vào**

## Cài đặt Mariadb 10.5
- MariaDB có thể được cài đặt từ trình quản lý gói yum của CentOS. Bạn cần thêm repository MariaDB vào hệ thống của mình trước khi cài đặt. Tạo một tệp repo mới bằng lệnh sau:

```sh
vi /etc/yum.repos.d/MariaDB.repo
```

- Sau đó thêm dòng sau vào tệp

```sh
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.5/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

- Cài đặt thêm gói epel-release

```sh
yum install -y epel-release
```


- Cập nhật hệ thống trước khi cài đặt mariadb

```sh
yum -y update
```

- Cài đặt Mariadb

```sh
yum install MariaDB-server MariaDB-client
```

- Tắt MariaDB (do liên quan tới cấu hình Galera MariaDB)

```
systemctl stop mariadb
```

**LƯU Ý: TRÊN TẤT CẢ 3 NODE ĐANG TỒN TẠI TRÊN CỤM CLUSTER TA CŨNG CẦN DỪNG MARIADB ĐỂ CẤU HÌNH GALERA CLUSTER THÊM NODE MỚI**

## Phần 3. Cấu hình Galera Cluster

- Sao chép tệp cấu hình server.cnf từ thư mục /etc/my.cnf.d/ và lưu trữ bản sao dự phòng dưới tên server.cnf.bak cũng trong thư mục đó (/etc/my.cnf.d/). Điều này giúp đảm bảo rằng bạn có một bản sao của tệp cấu hình gốc trước khi thực hiện bất kỳ thay đổi nào.

```sh
cp /etc/my.cnf.d/server.cnf /etc/my.cnf.d/server.cnf.bak
```

- Sau đó chỉnh sửa cấu hình trong file server.cnf

```sh
echo '[server]
[mysqld]
bind-address=192.168.249.173

[galera]
wsrep_on=ON
wsrep_provider=/usr/lib64/galera/libgalera_smm.so
#add your node private ips here
wsrep_cluster_address="gcomm://192.168.249.170,192.168.249.171,192.168.249.165,192.168.249.173"
binlog_format=row
default_storage_engine=InnoDB
innodb_autoinc_lock_mode=2
#Cluster name
wsrep_cluster_name="portal_cluster"
# Allow server to accept connections on all interfaces.
bind-address=192.168.249.173
# this server private ip, change for each server
wsrep_node_address="192.168.249.173"
# this server name, change for each server
wsrep_node_name="node4"
wsrep_sst_method=rsync
[embedded]
[mariadb]
[mariadb-10.2]
' > /etc/my.cnf.d/server.cnf
```

**LƯU Ý TẠI NODE1, NODE2, NODE3 CŨNG CẦN SỬA CẤU HÌNH TRONG FILE /ETC/MY.CNF.D/SERVER.CNF CHO PHÙ HỢP VỚI NODE MỚI ĐƯỢC THÊM VÀO**

- SAU ĐÓ TẠI NODE1 THỰC HIỆN KHỞI TẠO CLUSTER

```sh
galera_new_cluster
```

- Khởi động lại dịch vụ Mariadb

```sh
systemctl start mariadb
systemctl enable mariadb
```

- Tại 3 node còn lại chạy dịch vụ mariadb

```sh
systemctl start mariadb
systemctl enable mariadb
```

- KIỂM TRA TẠI NODE1

```
mysql -u root -e "SHOW STATUS LIKE 'wsrep_cluster_size'"
```

![Imgur](https://i.imgur.com/ZuREojT.png)


## Triển khai Haproxy Pacemaker cho Cluster Galera trên node mới

### Cài đặt Haproxy bản 1.8

- Cài đặt wget và socat từ kho lưu trữ của CentOS.

```sh
yum install wget socat -y
```

- Tải xuống gói RPM của HAProxy phiên bản 1.8.1 từ URL được cung cấp.

```
wget http://cbs.centos.org/kojifiles/packages/haproxy/1.8.1/5.el7/x86_64/haproxy18-1.8.1-5.el7.x86_64.rpm
```

- Cài đặt gói RPM HAProxy vừa tải xuống.

```sh
yum install haproxy18-1.8.1-5.el7.x86_64.rpm -y
```

- Tạo bản backup cho cấu hình mặc định và chỉnh sửa cấu hình HAproxy

```sh
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
    server node2 192.168.249.171:3306 check inter 5s fastinter 2s rise 3 fall 3 backup
    server node2 192.168.249.165:3306 check inter 5s fastinter 2s rise 3 fall 3 backup
    server node2 192.168.249.173:3306 check inter 5s fastinter 2s rise 3 fall 3 backup' > /etc/haproxy/haproxy.cfg
```


- Cấu hình Log cho HAProxy

```sh
sed -i "s/#\$ModLoad imudp/\$ModLoad imudp/g" /etc/rsyslog.conf
sed -i "s/#\$UDPServerRun 514/\$UDPServerRun 514/g" /etc/rsyslog.conf
echo '$UDPServerAddress 127.0.0.1' >> /etc/rsyslog.conf

echo 'local2.*    /var/log/haproxy.log' > /etc/rsyslog.d/haproxy.conf

systemctl restart rsyslog
```

- Bổ sung cấu hình cho phép kernel có thể binding tới IP VIP

```sh
echo 'net.ipv4.ip_nonlocal_bind = 1' >> /etc/sysctl.conf
```

- Tắt dịch vụ HAProxy

```sh
systemctl stop haproxy
systemctl disable haproxy
```

## Cài đặt pacemaker corosync

- Cài đặt gói pacemaker pcs

```ssh
yum -y install pacemaker pcs
```

```
systemctl start pcsd 
systemctl enable pcsd
```

- Thiết lập mật khẩu user hacluster (đặt giống mật khẩu như 3 node đã cài đặt)

```sh
passwd hacluster
```

- THÊM NODE MỚI VÀO CLUSTER

Chứng thực cluster (Chỉ thực thiện trên cấu hình trên một node duy nhất, trong bài sẽ thực hiện trên node1), nhập chính xác tài khoản user hacluster

```sh
pcs cluster auth node1 node2 node3 node4

Username: hacluster
Password: *********
```

![Imgur](https://i.imgur.com/5Yf2A7e.png)



- Khởi tạo cấu hình cluster ban đầu cho node mới 

```sh
pcs cluster setup --name ha_cluster node4
```

![Imgur](https://i.imgur.com/XC0rC6a.png)


- Khởi động Cluster

```sh
pcs cluster start --all
```

- TUY NHIÊN: SAU KHI KIỂM TRA TRẠNG THÁI CỦA CÁC NODE VẪN CHƯA THẤY NODE ĐƯỢC THÊM VÀO

![Imgur](https://i.imgur.com/Zg1ED0v.png)


- Thêm cấu hình node mới vào trong file cấu hình **corosync.conf** của các node trong cụm và cả node mới để cụm Galera Cluster có thể thêm được node mới vào

```sh
vi /etc/corosync/corosync.conf
```

```
totem {
    version: 2
    cluster_name: ha_cluster
    secauth: off
    transport: udpu
}

nodelist {
    node {
        ring0_addr: node1
        nodeid: 1
    }

    node {
        ring0_addr: node2
        nodeid: 2
    }

    node {
        ring0_addr: node3
        nodeid: 3
    }

    node {
        ring0_addr: node4
        nodeid: 4
    }

}

quorum {
    provider: corosync_votequorum
}

logging {
    to_logfile: yes
    logfile: /var/log/cluster/corosync.log
    to_syslog: yes
}
```

- Tuy nhiên sau khi thêm vào hệ thống đã nhận node mới nhưng lại bị lỗi cơ sở dữ liệu

![Imgur](https://i.imgur.com/7Yezsia.png)


![Imgur](https://i.imgur.com/25QC7ta.png)


## Khắc phục sự cố. 

Sau khi thêm node mới, ta kiểm tra trạng thái của Mariadb ở các node thì thấy báo lỗi như sau:

```sh
[root@node2 ~]# systemctl status mariadb
● mariadb.service - MariaDB 10.5.24 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
  Drop-In: /etc/systemd/system/mariadb.service.d
           └─migrated-from-my.cnf-settings.conf
   Active: failed (Result: exit-code) since Tue 2024-03-26 03:55:01 EDT; 5min ago
     Docs: man:mariadbd(8)
           https://mariadb.com/kb/en/library/systemd/
  Process: 1308 ExecStart=/usr/sbin/mariadbd $MYSQLD_OPTS $_WSREP_NEW_CLUSTER $_WSREP_START_POSITION (code=exited, status=1/FAILURE)
  Process: 976 ExecStartPre=/bin/sh -c [ ! -e /usr/bin/galera_recovery ] && VAR= ||   VAR=`cd /usr/bin/..; /usr/bin/galera_recovery`; [ $? -eq 0 ]   && systemctl set-environment _WSREP_START_POSITION=$VAR || exit 1 (code=exited, status=0/SUCCESS)
  Process: 964 ExecStartPre=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
 Main PID: 1308 (code=exited, status=1/FAILURE)
   Status: "MariaDB server is down"

Mar 26 03:55:00 node2 mariadbd[1308]: at /home/buildbot/buildbot/build/gcomm/src/pc.cpp:connect():160
Mar 26 03:55:00 node2 mariadbd[1308]: 2024-03-26  3:55:00 0 [ERROR] WSREP: /home/buildbot/buildbot/build/gcs/src/gcs_core.cpp:gcs_core_open():222:...timed out)
Mar 26 03:55:01 node2 mariadbd[1308]: 2024-03-26  3:55:01 0 [ERROR] WSREP: /home/buildbot/buildbot/build/gcs/src/gcs.cpp:gcs_open():1675: Failed t...timed out)
Mar 26 03:55:01 node2 mariadbd[1308]: 2024-03-26  3:55:01 0 [ERROR] WSREP: gcs connect failed: Connection timed out
Mar 26 03:55:01 node2 mariadbd[1308]: 2024-03-26  3:55:01 0 [ERROR] WSREP: wsrep::connect(gcomm://192.168.249.170,192.168.249.171,192.168.249.165) failed: 7
Mar 26 03:55:01 node2 mariadbd[1308]: 2024-03-26  3:55:01 0 [ERROR] Aborting
Mar 26 03:55:01 node2 systemd[1]: mariadb.service: main process exited, code=exited, status=1/FAILURE
Mar 26 03:55:01 node2 systemd[1]: Failed to start MariaDB 10.5.24 database server.
Mar 26 03:55:01 node2 systemd[1]: Unit mariadb.service entered failed state.
Mar 26 03:55:01 node2 systemd[1]: mariadb.service failed.
Hint: Some lines were ellipsized, use -l to show in full.
```

- Khi bị báo lỗi như vậy thì việc khởi động, hay chạy lại mariadb là không thể. Do đó ta cần khởi tạo lại cụm cluster. Để làm điều đó, trước tiên ta cần thay đổi giá trị **seqno** trong file **grastate.dat**. Và node có giá trị **seqno** lớn nhất sẽ là node khởi tạo lại cluster. 

```
[root@node1 ~]# cat /var/lib/mysql/grastate.dat
# GALERA saved state
version: 2.1
uuid:    f13047e6-e7f5-11ee-87a9-4e61fa2adef5
seqno:   -1
safe_to_bootstrap: 0
```

```
[root@node2 ~]# cat /var/lib/mysql/grastate.dat
# GALERA saved state
version: 2.1
uuid:    f13047e6-e7f5-11ee-87a9-4e61fa2adef5
seqno:   -1
safe_to_bootstrap: 0
```

```
[root@node3 ~]# cat /var/lib/mysql/grastate.dat
# GALERA saved state
version: 2.1
uuid:    f13047e6-e7f5-11ee-87a9-4e61fa2adef5
seqno:   -1
safe_to_bootstrap: 0
```

```
[root@node4 ~]# cat /var/lib/mysql/grastate.dat
# GALERA saved state
version: 2.1
uuid:    f13047e6-e7f5-11ee-87a9-4e61fa2adef5
seqno:   -1
safe_to_bootstrap: 0
```



Trong bài lab database chưa có sự đọc ghi dữ liệu nên seqno = -1 giống nhau ở các node.

Để khởi tạo lại cluster, thay đổi giá trị safe_to_bootstrap bằng 1 và chạy câu lệnh galera_new_cluster. Sau khi chạy câu lệnh **galera_new_cluster** cluster sẽ khởi tạo trở lại.

Thực hiện tại node1

```sh
vi /var/lib/mysql/grastate.dat
```

```
# GALERA saved state
version: 2.1
uuid:    f13047e6-e7f5-11ee-87a9-4e61fa2adef5
seqno:   -1
safe_to_bootstrap: 1
```

Sau đó khởi động lại mariadb

```
systemctl start mariadb
systemctl status mariadb
```

Khởi động lại dịch vụ mariadb ở các node còn lại

- Lúc này thì cluster sẽ lại hoạt động bình thường. 


![Imgur](https://i.imgur.com/zz6wjEc.png)



![Imgur](https://i.imgur.com/GAUnMBV.png)

