# Cách Backup và Restore trong Mariadb Replication

## Backup
Trước khi thực hiện backup ta vào trang quản lý wordpress tạo các bài viết để kiểm tra tính backup và restore database

![Imgur](https://i.imgur.com/MEiIbsR.png)

Để sao lưu tất cả các cơ sở dữ liệu trong hệ thống MariaDB, bạn có thể sử dụng công cụ `mysqldump` kết hợp với các tùy chọn để sao lưu toàn bộ cơ sở dữ liệu. Dưới đây là các bước bạn có thể thực hiện:

1. **Sử dụng mysqldump:**
   - Đăng nhập vào terminal hoặc command prompt trên máy chủ chứa cơ sở dữ liệu MariaDB.

2. **Sao lưu tất cả các cơ sở dữ liệu:**
   - Sử dụng lệnh `mysqldump` với tùy chọn `--all-databases` để sao lưu tất cả các cơ sở dữ liệu có trong hệ thống MariaDB. Ví dụ:

     ```sh
     mysqldump -u root -p --all-databases > all_databases_backup.sql
     ```

     Trong đó:
     - `username`: Tên người dùng có quyền truy cập để thực hiện sao lưu.
     - `all_databases_backup.sql`: Tên tệp sao lưu mà bạn muốn tạo ra.

   Lệnh này sẽ tạo ra một tệp sao lưu chứa toàn bộ cơ sở dữ liệu trong hệ thống MariaDB, bao gồm cả cấu trúc và dữ liệu của mỗi cơ sở dữ liệu.

3. **Lưu trữ tệp sao lưu:**
   - Tệp sao lưu được tạo ra (`all_databases_backup.sql`) có thể được lưu trữ trong bất kỳ nơi nào bạn muốn, như trên máy chủ hiện tại hoặc trên một máy chủ lưu trữ khác trong hệ thống của bạn.

4. **Quản lý tệp sao lưu:**
   - Đảm bảo rằng bạn lưu trữ tệp sao lưu một cách an toàn và có hệ thống để có thể phục hồi dữ liệu nếu cần.

Lưu ý rằng quá trình sao lưu toàn bộ cơ sở dữ liệu có thể tốn thời gian và tài nguyên, đặc biệt là khi cơ sở dữ liệu của bạn lớn. Hãy đảm bảo rằng bạn có đủ không gian lưu trữ và tài nguyên để thực hiện quá trình sao lưu một cách thành công.


Sau khi backup xong ta sẽ xóa hết các bài viết trên wordpress vừa tạo trên đi

![Imgur](https://i.imgur.com/B8Obzi6.png)

## Restore
Để khôi phục dữ liệu từ một tệp sao lưu đã tạo bằng `mysqldump`, bạn có thể sử dụng lệnh `mysql` để thực hiện việc này. Dưới đây là các bước bạn cần thực hiện để khôi phục dữ liệu từ tệp sao lưu:

1. **Đăng nhập vào terminal hoặc command prompt trên máy chủ chứa cơ sở dữ liệu MariaDB.**

2. **Khôi động MariaDB:**
   - Trước tiên, đảm bảo rằng dịch vụ MariaDB đang hoạt động để có thể khôi phục dữ liệu vào cơ sở dữ liệu. Nếu chưa khởi động, bạn có thể sử dụng lệnh sau:

     ```sh
     systemctl start mariadb
     ```

3. **Thực hiện khôi phục từ tệp sao lưu:**
   - Sử dụng lệnh `mysql` để khôi phục dữ liệu từ tệp sao lưu đã tạo. Ví dụ:

     ```sh
     mysql -u username -p < all_databases_backup.sql
     ```

     Trong đó:
     - `username`: Tên người dùng có quyền truy cập để thực hiện khôi phục.
     - `all_databases_backup.sql`: Tên tệp sao lưu mà bạn muốn khôi phục.

   Lệnh này sẽ đọc tệp sao lưu và thực hiện các câu lệnh SQL để khôi phục cơ sở dữ liệu trong MariaDB từ tệp sao lưu đó.

4. **Kiểm tra dữ liệu đã được khôi phục:**
   - Sau khi quá trình khôi phục hoàn tất, bạn có thể kiểm tra lại cơ sở dữ liệu để đảm bảo rằng dữ liệu đã được khôi phục đúng cách.

Lưu ý rằng quá trình khôi phục dữ liệu từ tệp sao lưu có thể mất một khoảng thời gian tùy thuộc vào kích thước của tệp sao lưu và tốc độ xử lý của máy chủ MariaDB. Đảm bảo rằng bạn đang thực hiện quá trình này trong một môi trường an toàn và đủ tài nguyên để tránh sự cố và mất mát dữ liệu.

Ta vào lại trang quản trị wordpress và đã thấy các bài viết vừa xóa đi đã quay trở lại

![Imgur](https://i.imgur.com/hGTidoq.png)