# Thực hiện Backup và Restore trong Zimbra

## 1.Backup

- Trước khi backup dữ liệu trong zimbra ta sẽ liệt kê tất cả các tài khoản trong zimbra đang tồn tại 

```
sudo -u zimbra /opt/zimbra/bin/zmprov -l gaa 
```

![Imgur](https://i.imgur.com/8tqtzFz.png)


- Tiếp đó ta tiến hành vào mailbox của một người dùng bất kì, sẽ thấy các email đang tồn tại

![Imgur](https://i.imgur.com/P2HjzjP.png)



- Sau đó chúng ta tiến hành tạo file backup

```
vi /srv/backup-mailbox.sh
```

- Điền những nội dung sau đây vào file backup

![Imgur](https://i.imgur.com/aDsUjHl.png)


- Ta cấp quyền cho file backup

```
chmod +x /srv/backup-mailbox.sh

```

- Sau đó chạy file để tạo backup

```
sh /srv/backup-mailbox.sh
```

![Imgur](https://i.imgur.com/y48XJwJ.png)


- Lúc này ta kiểm tra thư mục thì sẽ thấy dữ liệu của các tài khoản đã được backup

![Imgur](https://i.imgur.com/iS1SN7P.png)

- Ta tiến hành vào mailbox của một người dùng ở trên và xóa toàn bộ email đang tồn tại đi

![Imgur](https://i.imgur.com/Aoi121i.png)


## Backup

- Ta tiến hành tạo file restore dữ liệu

```
vi /srv/restore-mailbox.sh
```

- Sau đó điền nội dung sau vào: 

```
#!/bin/bash

BACKUPDIR="/srv/backup/080324";

clear

echo "Retrieve all zimbra user name..."

USERS=`su - zimbra -c 'zmprov -l gaa | sort'`;

for ACCOUNT in $USERS; do
NAME=`echo $ACCOUNT`;
echo "Restoring $NAME mailbox..."
su - zimbra -c "zmmailbox -z -m $NAME postRestURL '//?fmt=tgz&resolve=skip' $BACKUPDIR/$NAME.tgz";
done
echo "All mailbox has been restored sucessfully"
```


![Imgur](https://i.imgur.com/6kJGwet.png)

- Trong đó: /srv/backup/080324 đây là đường dẫn đến thư mục chứa các file backup

- Sau đó cấp quyền cho file

```
chmod +x /srv/restore-mailbox.sh
```

- Chạy file để restore dữ liệu: 

```
sh /srv/restore-mailbox.sh
```

![Imgur](https://i.imgur.com/p3BL5QS.png)

- Sau đó ta quay trở lại mailbox ở trên và đã thấy tất cả các email đã quay trở lại

![Imgur](https://i.imgur.com/0m4MMGI.png)


