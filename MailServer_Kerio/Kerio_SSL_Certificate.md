## Cài đặt chứng chỉ SSL cho Kerio
## Cài đặt
- Bạn có thể truy cập vào trang **https://www.ssls.com** để đăng kí lấy 1 chứng chỉ SSL

![Imgur](https://i.imgur.com/RdEFwvd.png)

- Chọn 1 chứng chỉ và đăng kí dùng thử

![Imgur](https://i.imgur.com/YnNh3rB.png)

- Chọn **ACTIVE**

![Imgur](https://i.imgur.com/fUnau8E.png)

- Nhập tên miền mà bạn muốn đăng kí chứng chỉ SSL

![Imgur](https://i.imgur.com/1D12H7R.png)


- Chọn **Use my CSR**, và copy dòng lệnh được tạo ra 

![Imgur](https://i.imgur.com/7gdZbNC.png)


- Chạy đoạn lệnh ở trên ở máy server

![Imgur](https://i.imgur.com/xpx2rnk.png)


- Copy đoạn **BEGIN CERTIFICATE REQUEST** vào phần **ENTER CSR** trên trình duyệt vầ ấn **ONWARDS**

![Imgur](https://i.imgur.com/AwXdjJ6.png)


- Chọn **Create a DNS record**

- Do lab trên VMware và dùng tên miền chưa được public lên không thể yêu cầu được chứng chỉ, Nên ở bước này sẽ không thể lấy được key của ssl

- Nhưng nếu là tên miền thật và đã lấy được Key và chứng chỉ của SSL thì ta tiếp tục làm như sau

- Đăng nhập bằng tài khoản quản trị admin, sau đó chuyển đến **Configuration >> SSL Certificates**

![Imgur](https://i.imgur.com/NHBzGtE.png)


- Import Certificate: Chọn mục Import >> Import a new Certificate…

![Imgur](https://i.imgur.com/1wcZJGo.png)


- Duyệt đến các file Key (.key) và Certificate (.crt) trên máy tính cục bộ rồi nhấn Import

![Imgur](https://i.imgur.com/1plgcv7.png)



