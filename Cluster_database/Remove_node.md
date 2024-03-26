## Xóa một node khỏi cụm Cluster

Để xóa một node khỏi cụm cluster Pacemaker, bạn cần thực hiện một số bước sau:

1. **Dừng dịch vụ MariaDB trên node đó (node mà bạn muốn xóa)**: Bạn cần đảm bảo rằng dịch vụ MariaDB trên node mục tiêu đã được ngừng trước khi tiến hành xóa node khỏi cụm. Bạn có thể dừng dịch vụ bằng lệnh:

    ```
    systemctl stop mariadb
    ```

   
2. **Thực hiện lệnh xóa node từ cụm trong node chính**:
   
    ```
    pcs cluster node remove node3
    ```

    Trong đó, `node3` là tên của node bạn muốn xóa khỏi cụm.


![Imgur](https://i.imgur.com/DTMxP9k.png)


3. **Kiểm tra lại tình trạng của cụm**: Sau khi xóa node khỏi cụm, hãy kiểm tra lại tình trạng của cụm để đảm bảo rằng việc xóa node đã được thực hiện thành công và cụm vẫn hoạt động bình thường.

Lưu ý rằng quá trình này có thể ảnh hưởng đến sự ổn định của cụm cluster, do đó hãy đảm bảo rằng bạn đã sao lưu dữ liệu quan trọng và kiểm tra kỹ lưỡng trước khi thực hiện các thay đổi.


![Imgur](https://i.imgur.com/KRULmqG.png)

- Node 3 đã không còn hoạt động và node1 và node2 vẫn hoạt động bình thường. Như vậy ta đã loại bỏ thành công node3 ra khỏi cụm cluster


## Xử lý sự cố
- Trong trường hợp tốt, sau khi ta đã loại bỏ 1 node đi thành công, và sau đó ta tắt máy khi và bật lại thì cụm cluster vẫn hoạt động bình thường. 

- Tuy nhiên, nếu khi ta bật lại bị lỗi database như sau: 

```
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

- Thì ta cần phải khắc phục sự cố

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

Trong bài lab database chưa có sự đọc ghi dữ liệu nên seqno = -1 giống nhau ở các node.

Để khởi tạo lại cluster, thay đổi giá trị safe_to_bootstrap bằng 1 và chạy câu lệnh galera_new_cluster. Sau khi chạy câu lệnh galera_new_cluster cluster sẽ khởi tạo trở lại.

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

Khởi động lại dịch vụ mariadb ở node 2

- Lúc này thì cluster sẽ lại hoạt động bình thường. 

