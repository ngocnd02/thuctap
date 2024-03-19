## Một số câu lệnh để quản lý HAProxy và Pacemaker cho cụm Galera Cluster trên Centos 7


1. **Quản lý Pacemaker**:
   - `pcs cluster setup`: Thiết lập một cụm Pacemaker.
   - `pcs status`: Kiểm tra trạng thái của cụm.
   - `pcs resource`: Quản lý các tài nguyên (resource) trong cụm.
   - `pcs constraint`: Quản lý các ràng buộc (constraints) giữa các tài nguyên.
   - `pcs property`: Cấu hình các thuộc tính cụm.
   - `pcs node`: Quản lý các nút trong cụm.

2. **Quản lý HAProxy**:
   - `systemctl start haproxy`: Khởi động dịch vụ HAProxy.
   - `systemctl stop haproxy`: Dừng dịch vụ HAProxy.
   - `systemctl restart haproxy`: Khởi động lại dịch vụ HAProxy.
   - `systemctl status haproxy`: Kiểm tra trạng thái của dịch vụ HAProxy.
   - `haproxy -c -f /etc/haproxy/haproxy.cfg`: Kiểm tra cấu hình HAProxy.

3. **Quản lý Galera Cluster**:
   - `mysql -u <user> -p`: Truy cập vào cơ sở dữ liệu MySQL trên các nút Galera.
   - `SHOW STATUS LIKE 'wsrep_cluster_size';`: Kiểm tra kích thước của cụm Galera.
   - `SHOW STATUS LIKE 'wsrep_cluster_status';`: Kiểm tra trạng thái của cụm Galera.
   - `SHOW STATUS LIKE 'wsrep_local_state_comment';`: Kiểm tra trạng thái của nút hiện tại trong cụm Galera.

4. **Kiểm tra Logs**:
   - `/var/log/messages`: Kiểm tra log chung của hệ thống.
   - `/var/log/haproxy.log`: Log của HAProxy.
   - `/var/log/pcsd/pcsd.log`: Log của Pacemaker.

5. **Cấu hình và Mở rộng**:
   - Sử dụng các tệp cấu hình `/etc/haproxy/haproxy.cfg`, `/etc/pacemaker/pacemaker.conf` để thực hiện cấu hình và mở rộng hệ thống theo yêu cầu.

Quản trị viên cần hiểu rõ về mỗi câu lệnh và công cụ, cũng như là cách sử dụng chúng để quản lý và giám sát cụm. Đồng thời, cũng cần thường xuyên kiểm tra và giám sát các log để phát hiện và xử lý các vấn đề một cách kịp thời.