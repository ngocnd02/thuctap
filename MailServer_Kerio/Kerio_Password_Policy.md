## Chính sách mật khẩu trong Kerio
Để bảo vệ người dùng và mật khẩu của họ trong Kerio Connect:
- 1. Khuyến khích người dùng tạo mật khẩu mạnh.

- 2. Yêu cầu mật khẩu phức tạp (đối với người dùng cục bộ).

- 3. Bật hết hạn mật khẩu (đối với người dùng cục bộ).

- 4. Bảo vệ khỏi việc đoán mật khẩu đăng nhập.

- 5. Tạo mật khẩu người dùng mạnh mẽ.

### Tạo mật khẩu người dùng mạnh
   
Mật khẩu người dùng mạnh mẽ nên dài và phức tạp. Các hướng dẫn sau có thể giúp bạn khuyến khích người dùng của mình:

Dài
- Mật khẩu nên có ít nhất 8 ký tự.

Phức tạp
- Mật khẩu nên chứa tất cả các yếu tố sau:
  - Chữ thường
  - Chữ hoa
  - Số
  - Ký tự đặc biệt

Người dùng nên thay đổi mật khẩu của họ thường xuyên.

### Tạo mật khẩu mạnh
Kerio Connect có thể tạo mật khẩu mạnh cho người dùng. 
- 1.Tới phần **Users**

- 2. Chọn một user và click **Edit**.

- 3. Trong phần tab **General**, chọn **Generate**

![Imgur](https://i.imgur.com/Qwx1ZWz.png)


- 4. Copy mật khẩu đó và đưa lại cho người dùng. 


### Yêu cầu mật khẩu phức tạp (Đối với người dùng)
- Trong Kerio Connect, bạn có thể buộc người dùng phải tạo mật khẩu mạnh và phức tạp. 

- Để cấu hình mật khẩu phức tạp cho từng domain:

	- Trong giao diện quản trị, điều hướng đến mục **Configuration > Domains**.

	- Chọn một domain và nhấp vào **Edit**.

	- Trên tab **Security**, bật tùy chọn **User passwords must meet complexity requirements**.

	- Nhấp OK.


![Imgur](https://i.imgur.com/frvrAfk.png)


### Bảo vệ chống lại các cuộc tấn công đoán mật khẩu

- Kerio Connect có thể chặn địa IP nghi ngờ thực hiện các cuộc tấn công đoán mật khẩu (mười lần thất bại trong một phút).

	- Điều hướng đến mục **Configuration > Security > tab Security Policy**.

	- Chọn tùy chọn **Block IP addresses suspicious of password guessing attacks**.

**Lưu ý:** Địa chỉ IP bị chặn đối với từng dịch vụ cụ thể. Nếu POP3 bị chặn, kẻ tấn công có thể thử đăng nhập qua IMAP.

	- Bạn có thể chọn một nhóm địa chỉ IP đáng tin cậy.

	- Để chặn tất cả các dịch vụ, kiểm tra tùy chọn **Block user accounts probably targeted by password guessing** để khóa các tài khoản bị ảnh hưởng.

	- Nhấp OK.

![Imgur](https://i.imgur.com/3AuSUWu.png)



### Bật hết hạn mật khẩu (đối với người dùng cục bộ)
- Để bảo vệ mật khẩu người dùng cục bộ, bạn có thể bật chức năng hết hạn mật khẩu.

	- Trong giao diện quản trị, điều hướng đến mục **Configuration > Domains**.

	- Chọn một domain và nhấp vào **Edit**.

	- Trên tab **Security**, bật tùy chọn **User must change password every**.

	- Đặt số ngày sau khi người dùng phải thay đổi mật khẩu của họ.

	- Nhấp OK.

![Imgur](https://i.imgur.com/CiniHly.png)