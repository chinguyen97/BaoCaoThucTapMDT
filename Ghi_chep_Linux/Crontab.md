## Crontab 

### 1. Giới thiệu

Crontab là 1 tiện ích giúp lập lịch chạy các tác vụ trong hệ thống Linux theo các khoảng thời gian ấn định. 

Crontab đc dùng trong nhiều trường hợp. Ví dụ:
	- Gửi mail tới các user 
	- Xóa bỏ file cache hàng tháng
	- Backup cơ sử dữ liệu.
	- .....

- Cài đặt cron: 
	Hầu hết tất cả các VPS đều cài đặt sẵn `crontab`, Tuy nhiên vẫn có trường hợp VPS không có. 

Sử dụng lệnh: 

`yum install cronie`

Start crontab và tự động chạy mỗi khi reboot:

```
service crond start
chkconfig crond on
```
### 2. Câu lệnh 

- Một số lệnh thường dùng: 
	- `crontab -e` Tạo và chỉnh sửa file crontab 
	- `crontab -l` Hiển thị file crontab
	- `crontab -r` Xóa file crontab
	- `service crond status` hoăc `systemctl status crond`: Kiểm tra trạng thái cron 
	- Khởi động, khởi động lại, dừng dịch vụ  cron thì thay status bằng start , restart, stop. 

- Nơi lưu trữ các cấu hình cron  `/var/spool/cron/`

Mặc định thì được lưu trữ tại đây nhưng tùy hệ thống có thể lưu ở các vị trí khác

### 3.  Định dạng dòng crontab

Cú pháp: 
`*[phút]  *[giờ] *[ngày] *[tháng] *[thứ] [lệnh]`

Mỗi dòng thường gồm 6 trường. 5 trường đầu tiên xác định thời điểm chạy lênh. Trường 6 là lệnh chạy. Sunday =0

- Nếu không khai báo số cụ thể thì sẽ để \* , Ký tự này được hiểu là tất cả các thời gian. 

- Dấu **,**, để thiết lập nhiều điểm thời gian. 

Ví dụ : `20, 40 * * * * <command>`

	Lệnh này có nghĩa là vào phút thứ 20 và 40 lệnh sẽ chạy. 

- Dấu **/** để chia thời gian chạy

Ví dụ: `*/5 * * * * <scan system now>`

	5 phút hệ thống sẽ quét 1 lần để kiểm tra điều bất thường. 

- Dấu **-** chỉ khoảng thời gain: 

Ví dụ: `30 10-12 * * * <command>`
	Vào 10h30 11h30 12h30 hệ thống sẽ chạy. 

- Có thể dùng @reboot để chạy lệnh nào đó khi mà server boot lại. Chẳng hạn khởi động một số chương trình không tự khởi động lại được khi server bị reboot.

`@reboot <start some program>`

- Các thiết lập đặc biệt khác
	- @hourly : chạy hàng giờ vào phút thứ 0
	- @daily : chạy hàng ngày vào 00:00
	- @monthy : chạy hàng tháng vào 00:00 của ngày đầu tiên của mỗi tháng
	- @yearly : chạy hàng năm vào 00:00 của ngày đầu tiên của mỗi năm

 
- `service crond restart` Hoặc `systemctl restart crond.service` để khởi động lại service cho crontab mới chính thức có hiệu lực.

### 4. Ví dụ

Cách 1: 
Edit file  `/etc/crontab`

```
[root@localhost etc]# cat crontab
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed


45 * * * * root reboot 
```

Hoặc `crontab -e`

Sử dụng đường dẫn tuyệt đối. ` */5 * * * * /usr/sbin/reboot`

```
[root@localhost etc]# which reboot
/usr/sbin/reboot
```

`[root@localhost user]# tailf /var/log/cron`


**Tài liệu tham khảo**
[1] https://hocvps.com/tong-quat-ve-crontab/
[2] https://forum.gocit.vn/threads/s-dung-crontab-tren-linux.428/