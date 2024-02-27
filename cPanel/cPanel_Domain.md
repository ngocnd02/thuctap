## Domains

### Create a new Domain
**Chú Ý**
- Để tạo một miền mới, nhà cung cấp dịch vụ lưu trữ của bạn phải kích hoạt ít nhất một trong những tính năng sau trong giao diện Quản lý Tính Năng của WHM (WHM » Home » Packages » Feature Manager):

	- Addon Domains (Miền Bổ Sung)

	- Aliases (Bí danh)

	- Subdomains (Miền phụ)

![Imgur](https://i.imgur.com/65h0sDC.png)

- Tai phần **Add a new feature list** Nhập **Addon Doamins** và ấn **Add feature List**

![Imgur](https://i.imgur.com/nkY6NmE.png)

- Để tạo một miền, thực hiện các bước sau:

1. Vào **cPanel >> Domains >> Create a New Doamin**. Một giao diện mới sẽ xuất hiện.

![Imgur](https://i.imgur.com/guT9Pdo.png)

2. Nhập tên miền đầy đủ vào ô văn bản Tên Miền.

3. Để tạo một miền mới, nhập tên miền mới. Ví dụ, example.com.

![Imgur](https://i.imgur.com/lIWeClh.png)

4. Để tạo một miền phụ, nhập một tên mới, sau đó là một dấu chấm (.) và sau đó là tên miền của trang web. Ví dụ, nhập subdomain.example.com để tạo một miền phụ của example.com.

5. Tuỳ chọn, bạn có thể chỉ định thư mục nơi bạn muốn các tệp tin cho miền tồn tại (thư mục gốc của miền). Để tạo thư mục này, hủy chọn hộp kiểm Chia sẻ thư mục gốc với "example.com", trong đó example.com đại diện cho miền chính của bạn. Bạn không thể tạo thư mục gốc ngoài thư mục public_html/. Điều này sẽ tạo ra một addon domain.

### Redirect
- Giao diện Chuyển hướng cho phép bạn chuyển hết tất cả các khách truy cập của một tên miền hoặc trang cụ thể đến một URL khác. Ví dụ, nếu bạn tạo một trang với một URL dài, sử dụng giao diện Chuyển hướng để thêm một chuyển hướng từ một URL ngắn đến URL dài. Khách truy cập có thể nhập URL ngắn để truy cập nội dung của URL dài.

- Lưu Ý: Bạn không thể chỉnh sửa một chuyển hướng. Để sửa đổi một chuyển hướng, bạn phải xóa nó và sau đó tạo lại.

**Add a redirect**
1. Chọn một loại chuyển hướng từ menu Loại.

- Permanent (301) — Cài đặt này thông báo cho trình duyệt của khách truy cập để cập nhật bản ghi của nó.
  
- Temporary (302) — Cài đặt này không cập nhật các đánh dấu trang của khách truy cập.

2. Chọn một tên miền từ menu, hoặc chọn **All Public Domain** để chuyển hướng tất cả các tên miền mà tài khoản cPanel của bạn kiểm soát.

3. Trong ô tiếp theo, nhập phần còn lại của URL mà bạn muốn máy chủ chuyển hướng người truy cập. Ví dụ, nếu bạn muốn chuyển hướng từ http://example.com/directory.file.html đến một URL khác, hãy nhập directory/file.html trong ô văn bản này.

4. Trong ô **Redirect to**, nhập URL mà bạn muốn chuyển hướng người dùng đến.

- Lưu ý: Bạn bắt buộc phải chỉ định giao thức mà trang web bạn muốn chuyển hướng tới, ví dụ: https://, http://, ftp://

5. Chọn một trong những cài đặt sau:

- **Only redirect with www**: Cài đặt này chỉ chuyển hướng cho khách truy cập nhập tiền tố www. trước phần tên miền của URL.

- **Redirect with or without www**: Cài đặt này chuyển hướng tất cả người dùng, không phụ thuộc vào việc khách truy cập nhập tiền tố www. trước phần tên miền của URL.

- **Do not redirect www**:Cài đặt này không chuyển hướng cho người dùng nhập tiền tố www. trước phần tên miền của URL.

Chú Ý:
Giao diện vô hiệu hóa cài đặt chuyển hướng www. nếu bạn chọn **Tất Cả Các Tên Miền Công Cộng**.

6. Chọn cài đặt **Wild Card Redirect** nếu bạn muốn chuyển hướng tất cả các tệp trong một thư mục đến cùng tên tệp trong thư mục mới. Ví dụ, nếu bạn kích hoạt cài đặt Chuyển hướng Wild Card và example1.com chuyển hướng đến example.com, thì một khách truy cập cố gắng truy cập URL http://example1.com/pic.jpg sẽ được chuyển hướng đến URL http://example.com/pic.jpg.

7. Click **Add*.

![Imgur](https://i.imgur.com/1mPAy9K.png)

**Xóa redirect**

- Trong **cPanel >> Home >> Domains >> Redirect** phần Current Redirect chọn redirect muốn xóa và ấn **Delete**

![Imgur](https://i.imgur.com/YJgzv3h.png)

![Imgur](https://i.imgur.com/cVtOSkF.png)
