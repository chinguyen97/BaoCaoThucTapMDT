## System Logging


###. 1 Giới thiệu

System logging rất quan trọng trong việc khắc phục sự cô skhi có sai xót xảy ra. Logs lưu giữ ca shoatj động của hệ thống, bao gồm cả nhân, tiên strinhf boot, và cac sdichj vụ khác đang chạy. Ngoài logs, còn có một số tiện ích có thể giám sát và check status hệ thống. 

- ứng dụng của log:
	- Phân tích nguyên nhân khi có sự cố xảy ra. 
	- Khắc phục sự cố nhanh hơn
	- Phát hiện và dự đoán vân sđề

Mặc định file log sẽ được lưu trong thư mục /var/log/ và được lưu riêng rẽ từng tác vụ trong hệ thống. Ví dụ tiến trình boot sẽ được lưu trong file boot.log

```
[root@centos7 log]# ls
anaconda  boot.log-20190515  dmesg      grubby_prune_debug  messages  spooler   wtmp
audit     btmp               dmesg.old  lastlog             rhsm      tallylog
boot.log  cron               firewalld  maillog             secure    tuned

```

Các file log là file `clear text` nên có thể xem dễ dàng bằng các câu lệnh: more, tail, head, tail -f. 


### 2. file cấu hình syslog

File cấu hình là /etc/rsyslog.conf. Bởi vì logging vào 1 phần quan trọng của hệ điều hành, nên mặc định được cài đặt như 1 phần cảu gói lõi. 
Tuy nhiên vẫn nên kiểm tra lại: 
```
[root@centos7 log]# rpm -qa | grep syslog
rsyslog-8.24.0-34.el7.x86_64
```
Hoặc
```
[root@centos7 log]# yum list installed | grep syslog
rsyslog.x86_64                        8.24.0-34.el7                    @anaconda
```
Gói tin đã được cài đặt, cần kiểm tra các điều sau: 
- Thứ 1: Đảm bảo rằng dịch vụ được thiết lập dderaaer bắt đầu khi hệ thống khởi động. 
```
[root@rhel68-02 log]# chkconfig rsyslog --list
rsyslog        	0:off	1:off	2:on	3:on	4:on	5:on	6:off
```
```
[root@centos7 log]# systemctl list-unit-files | grep rsyslog
rsyslog.service                               enabled 
```

- Thứ 2: Đảm bảo rằng dịch vụ giờ đang chạy. 
```
[root@rhel68-02 log]# service rsyslog status
rsyslogd (pid  1640) is running...
```

- File /etc/rsyslog.conf được chia thành các phần sau: 
	- **Modules**: Cho biết liệu cúng có tể load hoặc unload (rsyslog is a module)
	- **Global directives**: Chỉ định các tùy chọn cấu hình áp dụng cho deamon.
	- **Rules**: Gồm a selector and an action
	- **Selector**: Cú pháp `<facility>.<priority>`
	- **Active**: Xác định vị trí lưu trữ log

```
# The authpriv file has restricted access.
authpriv.*                                              /var/log/secure
```

Rule được chia thành 2 trường như trện. 
- Trường 1: (Bên trái) Trường Seletor
	- Chỉ ra nguồn tạo ra log và mức cảnh báo cảu log đó.
	- Gồm 2 thành phần và được tách nhau bằng dấu "."
Các nguồn tạo ra log

|Nguồn | Ý nghĩa|
|----|----|
|kernel	|Log do kernel sinh ra|
|auth hoặc authpriv|Log do quá trình đăng nhập hoặc xác thực tài khoản|
|mail	|Log của mail|
|cron	|Log từ tiến trình cron trong hệ thống|
|user	|Log từ ứng dụng của người dùng|
|lpr	|Log từ hệ thống in ấn|
|deamon	|Log từ các tiến trình chạy trên nền của hệ thống|
|ftp	|Log từ tiến trình ftp|
|local 0 -> local 7|Log dự trữ cho sử dụng nội bộ|

Các mức cảnh báo:

|Mức cảnh báo|	Ý nghĩa|
|----|----|
|emerg|	Thông báo tình trạng khẩn cấp|
|alert|	Hệ thống cần can thiệp ngay|
|crit|	Tình trạng nguy kịch|
|error|	Thông báo lỗi đối với hệ thống|
|warn|	Mức cảnh báo đối với hệ thống|
|notice|	Chú ý đối với hệ thống|
|info|	Thông tin của hệ thống|
|debug|	Quá trình kiểm tra hệ thống|

- Trường 2: (Bên phải)
Chỉ ra nơi lưu trữ log của tiến trình đó. 

### Log Rotation (tltk)

***Tài liệu tham khảo***: 
[1] https://github.com/hocchudong/Syslog


