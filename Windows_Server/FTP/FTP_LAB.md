# Cài đặt FTP Server trên máy chủ Windows Server 2022

## Cài đặt FTP Server
- Trên windows server Internet Information Services (IIS) có hỗ trợ triển khai FTP server. Vì vậy, chúng ta sẽ tiến hành cài đặt IIS. 
- Trong Server Manager, chọn **Add roles and features**

![Imgur](https://i.imgur.com/UVhArGL.png)

- Tiếp tục chọn next, và chọn Web Server (IIS)

![Imgur](https://i.imgur.com/sf0HviK.png)

- Trong quá trình cài đặt, chọn thêm tùy chọn cài đặt **FTP Server**
- Cuối cùng, nhấn Install để cài đặt. 

![Imgur](https://i.imgur.com/UzMZWv8.png)

- Đây là giao diện của IIS

![Imgur](https://i.imgur.com/UBkaHEq.png)

## Tạo nhóm và người dùng. 
- Tạo nhóm và người dùng để có thể truy cập vào thư mục mà ta chia sẻ qua FTP Server
- Trong windows server, vào **Computer Management**

![Imgur](https://i.imgur.com/wLuzkWZ.png)

- Chọn mục **Local User and Groups**

![Imgur](https://i.imgur.com/u9Wtlx9.png)

- Trong mục Groups tạo một group mới

![Imgur](https://i.imgur.com/0JMPX0k.png)

- Trong mục Users tạo một người dùng mới

![Imgur](https://i.imgur.com/it0E0g5.png)

- Quay trở lại thư mục Groups, trong group **MHT**, thêm user mà ta vừa tạo vào group

![Imgur](https://i.imgur.com/BLRlV0k.png)

![Imgur](https://i.imgur.com/j6zyhMa.png)

## Tạo thư mục để chia sẻ
- Trong ổ đĩa C hoặc ổ đĩa bất kì nào bạn muốn tạo một thư mục, ở đây chúng ta tạo một thư mục **DATA FTP**, trong thư mục này tạo tiếp một thư mục **65MHT**
- Tiếp theo, chúng ta sẽ thiết lập quyền chia sẻ cho các thư mục này để có thể chia sẻ qua FTP Server.
- Kích chuột phải vào thư mục DATA FTP, chọn Sharing

![Imgur](https://i.imgur.com/d7BItmb.png)

- Tiếp theo, chọn Advanced Sharing..

![Imgur](https://i.imgur.com/NMSc8JY.png)

- Tích chọn Share this folder, và bấm chọn phầm Permissions

![Imgur](https://i.imgur.com/9OlhaYx.png)

- Ta thêm full quyền cho thư mục này

![Imgur](https://i.imgur.com/BlF2LRg.png)

- Tiếp theo, vào thư mục **65MHT** trong thư mục **DATA FTP**, kích chuột phải chọn phần **Secuirty**, trong đó chọn **Advance**

![Imgur](https://i.imgur.com/danaz6z.png)

- Tiếp đó, chọn **Disable inheritance**

![Imgur](https://i.imgur.com/o4OXa2v.png)

- Chọn Convert inherited...

![Imgur](https://i.imgur.com/hrruUzC.png)

- Vẫn trong phần **Security** chọn phần Users(...) và chọn **Edit**

![Imgur](https://i.imgur.com/huYMq4C.png)

- Chọn Users(..) và bấm Remove

![Imgur](https://i.imgur.com/uU9PCXu.png)

- Tiếp theo, thêm tên người dùng, hoặc nhóm cụ thể mà bạn muốn chia sẻ thư mục này vào

![Imgur](https://i.imgur.com/CWgFw8S.png)

- Thêm tên người dùng ta vừa tạo ở trên và ấn checkname, sau đó ấn oke

![Imgur](https://i.imgur.com/353ydky.png)

- Tiếp theo cấp quyền cho thư mục này

![Imgur](https://i.imgur.com/6V0hKPN.png)

## Tạo một trang FTP trên IIS
- Trong IIS Manager kích chuột phải vào phần Site và chọn Add FTP Site..

![Imgur](https://i.imgur.com/PWFZLsl.png)

- Điền tên của trang FTP, và trỏ đường dẫn tới thư mục muốn chia sẻ.

![Imgur](https://i.imgur.com/yXX3zZG.png)

- Điền địa chỉ IP của máy chủ FTP server, và tích chọn No SSL

![Imgur](https://i.imgur.com/DXULKbO.png)

- Trong phần **Authentication** chọn Basic, trong **Authorization** chọn Specified roles or user groups và điền thêm Administrator. và cấp quyền Read and Wirte. 

![Imgur](https://i.imgur.com/IHWOnRQ.png)

- Lúc này, ở máy client ta đã có thể chia sẻ vào file mà FTP server chia sẻ thông qua tài khoản Administrator. Ta có thể dùng Filezilla để truy cập hoặc vào this pc và nhập địa chỉ máy chủ FTP server để đăng nhập

![Imgur](https://i.imgur.com/xfePAyw.png)

- Ta đã thấy thư mục được chia sẻ hiện lên trong máy

![Imgur](https://i.imgur.com/g0smBX0.png)

- Tuy nhiên, đây là tài khoản Adminstrator, là tài khoản quản trị cao nhất có thể truy cập vào mọi thư mục, và ta không muốn cấp tài khoản quản trị này cho bất kì ai. Mà ở đây ta chỉ muốn chia sẻ thư mục 65MHT cho những người dùng thuộc nhóm MHT mà ta đã vừa tạo ở trên. Chính vì vậy, ta tiếp tục vào IIS Manager để cấu hình. 

- Trong trang FTP_SHARE mà ta vừa tạo trong IIS Manager, chọn phần **FTP Authorization Rules**

![Imgur](https://i.imgur.com/4pndKdZ.png)

- Chọn Add Alow Rule..

![Imgur](https://i.imgur.com/Ig5E1Zp.png)

- Điền tên group mà ta muốn có thể truy cập vào thư mục, và chọn OK

![Imgur](https://i.imgur.com/tQrQ6Vr.png)

- Lúc này ta tiến hành truy cập file FTP bằng tài khoản ta vừa tạo ở trên kia thuộc group MHT

![Imgur](https://i.imgur.com/bsuZgnq.png)

- Vào và ta đã thấy thư mục được chia sẻ. 

![Imgur](https://i.imgur.com/3Ti6ysh.png)

- Ở máy client, thêm một tệp tin để kiểm tra xem có chia sẻ được file không, ta tạo một tệp tin

![Imgur](https://i.imgur.com/Zzk9fsO.png)

- Quay trở lại Windows server và ta đã thấy tệp tin vừa tạo đã xuất hiện

![Imgur](https://i.imgur.com/n19WSYl.png)
