## Create/Restore Backup
- Với DA có 3 loại tài khoản người dùng là Admin, Reseller, và User tương ứng với 3 kiểu backup. 
- Nếu backup ở tài khoản Admin thì toàn bộ dữ liệu của Admin,  reseller và user cũng sẽ được backup, với tài khoản Reseller thì backup được dữ liệu của chính nó và các tài khoản user thuộc sở hữu của reseller. Và cuối cùng nếu backup ở tài khoản user thì nó chỉ có thể backup dữ liệu của chính user đó mà thôi. 

### Admin backup
- Tại trang chủ chính của Admin, chọn **Admin Backup/Transfer**

![Imgur](https://i.imgur.com/ab4fq6m.png)

- Có 5 bước để backup. Bước đầu chọn đối tượng backup, bạn có thể chọn tất cả user, hoặc chọn tất cả user nhưng ngoại trừ một số user, hoặc chỉ backup những user được chọn. Bước 2 chọn thời gian backup, có thể chọn backup ngay bây giờ hoặc, chọn thời gian cụ thể cho hoạt động backup. Bước 3 chọn vị trí lưu file backup. Bước 4, Lựa chọn loại dữ liệu bạn muốn backup. Và cuối cùng Bước 5 ấn submit để tiến hành backup. 

![Imgur](https://i.imgur.com/haffLph.png)


![Imgur](https://i.imgur.com/TeOxX0r.png)


![Imgur](https://i.imgur.com/Ca5540n.png)



### Reseller backup

- Thao tác tương tự như Admin backup

### User backup
- Trước tiên ta tạo các bài viết ở trên trang web để kiểm tra sau khi backup dữ liệu. 

![Imgur](https://i.imgur.com/W0ubzKj.png)


- Tại menu chính của User chọn **Create/Restore Backups**

![Imgur](https://i.imgur.com/SJcr0e3.png)

- Chọn những dữ liệu bạn muốn backup, sau đó ấn **Create Backup**

![Imgur](https://i.imgur.com/vRug5J4.png)

- Sau khi backup thành công DA sẽ có thông báo

![Imgur](https://i.imgur.com/sdPDaVT.png)

![Imgur](https://i.imgur.com/G3BfLJ8.png)

- Vào File Manager sẽ thấy thư mục backup đã được tạo và chưa file backup dữ liệu của user

![Imgur](https://i.imgur.com/5FwBymD.png)


- Tiếp theo ta tiến hành xóa một số bài viết ta vừa tạo ở trang web

![Imgur](https://i.imgur.com/4eGnRRm.png)

- Sau đó ta tiến hành restore lại dữ liệu . Tại menu chính của user chọn **Create/Restore Backup** sau đó chọn **Select a File to Restore** và restore file mà ta muốn. 

![Imgur](https://i.imgur.com/9EFuNRp.png)

- Chọn những dữ liệu mà ta muốn khôi phục 

![Imgur](https://i.imgur.com/wkEsMgb.png)

- Sau khi thành công sẽ có thông báo

![Imgur](https://i.imgur.com/o5J8S3h.png)

- Lúc này ta quay trở lại trang quản trị bài viết đã thấy đầy đủ các bài viết

![Imgur](https://i.imgur.com/NenyuTx.png)


 