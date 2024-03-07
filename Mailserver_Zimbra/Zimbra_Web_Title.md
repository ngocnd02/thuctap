## Thay đổi title cho website trong Zimbra

### Thay đổi title cho website dành cho client
- Ở đây chúng ta sẽ đổi title cho mailbox webapp và login mailbox webapp 

- Trước khi thay đổi: 

![Imgur](https://i.imgur.com/VD119Gc.png)


![Imgur](https://i.imgur.com/78xUYqT.png)


- Để có thể thay đổi được ta phải chỉnh sửa trong file **ZmMsg.properties** trong đường dẫn **/opt/zimbra/jetty/webapps/zimbra/WEB-INF/classes/messages**

```
cd /opt/zimbra/jetty/webapps/zimbra/WEB-INF/classes/messages

vi ZmMsg.properties
```

- Tìm và sửa trường **zimbraLoginTitle** và trường **zimbraTitle**. Trong đó, trường zimbraLoginTitle sẽ là hiển thị ở trang login khi ta muốn đăng nhập vào mail cá nhân. còn trường zimbraTitle sẽ hiển thị ở trong mailbox khi chúng ta đã đăng nhập vào mail cá nhân. 

![Imgur](https://i.imgur.com/bPEwlXX.png)


- Cuối cùng khởi động lại zimbra

```
zmcontrol restart
```

- Sau đó ta vào lại trang web để xem sự thay đổi

![Imgur](https://i.imgur.com/2HMWL6D.png)

![Imgur](https://i.imgur.com/w8VssJp.png)


### Thay đổi title website dành cho admin

- Trước khi thay đổi: 

![Imgur](https://i.imgur.com/yavKUTm.png)

- Để thay đổi ta phải chỉnh sửa title trong file **ZabMsg.properties** trong đường dẫn **/opt/zimbra/jetty_base/webapps/zimbraAdmin/WEB-INF/classes/messages**

```
cd /opt/zimbra/jetty_base/webapps/zimbraAdmin/WEB-INF/classes/messages

vi ZabMsg.properties
```

![Imgur](https://i.imgur.com/Tf30vl9.png)


- Sau đó ta khởi động lại zimbra

```
zmcontrol restart
```

- Sau đó ta vào lại web quản trị để thấy sự thay đổi.

![Imgur](https://i.imgur.com/Z12mkhW.png)