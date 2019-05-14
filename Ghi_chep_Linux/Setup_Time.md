## Setup time

Hệ thống vận hành phân biệt giữa 2 loại clock sau: 
	- A real-time clock (RTC): Thường được gọi là đồng hồ phần cứng (thường là 1 mạch tích hợp trong bo mạch hệ thống) hoàn toàn độc lập với trạng thái hiện tại của hệ điều hành  và chạy ngay cả khi tắt máy.
	- A system clock, đồng hồ phần mềm, được duy trì bởi nhân, và giá trị ban đầu của nó được dựa trên đồng hồ thời gian thực. Khi hệ thống khởi động và đồng hồ hệ thống được khởi tạo, đồng hồ hệ thống hoàn toàn độc lập với đồng hồ thời gian thực. 

Thời gian hệ thống luôn được gữ trong UTC (thời gian quốc tế) và được chuyển đổi sang h địa phương khi cần. Giờ địa phương là múi giờ (timezone) mà bạn thiết lập. Đồng hồ thời gian thực(RTC) có thể sử dụng UTC hoặc localtime. 

### 1. Command `timedatectl`

Tiện ích `timedatectl` được phân hối như 1 phần của hệ thống `ystemd`

- Hiển thị thời gian hiện tại

```
[root@redhat dir1]# timedatectl
      Local time: Tue 2019-05-14 10:52:16 ICT
  Universal time: Tue 2019-05-14 03:52:16 UTC
        RTC time: Tue 2019-05-14 03:52:28
       Time zone: Asia/Ho_Chi_Minh (ICT, +0700)
     NTP enabled: n/a
NTP synchronized: no
 RTC in local TZ: no
      DST active: n/a
```
NTP: Network Time Protocol

- Thay đổi time

`timedatectl set-time HH:MM:SS`

Lệnh này cập nhật cả thời gian hệ thống và đồng hồ phần cứng. Kết quả tương tự như `date --set` và `hwclock --systohc`

Lệnh này sẽ không thành công nếu NTP service được kích hoạt. 

Dịch vụ NTP có thể được enabled và disabled bằng command.
`timedatectl set-ntp boolean`
Boolean =yes (enable) =no(disable)

Lệnh này thất bại nếu 1 dịch vụ NTP chưa được cài đặt. 

Mặc định, hệ thống cấu hình sử dụng UTC. Để cấu hình hệ thống duy trì đồng hồ local time, chạy lệnh `timedatectl` với tùy chọn `et-local-rtc boolean`

Thay thế `boolen` bằng yes(or, alternatively, y, true, t, or 1). Để sử dụng UTC, thay thế `boolean` bằng no (or, alternatively, n, false, f, or 0).

- Thay đổi Date 

`timedatectl set-time YYYY-MM-DD`	

Lưu ý: Việc thay đổi ngày tháng sẽ dẫn đến thời gian đổi về 00:00:00
Để giữ thời gian hiện tại sử dụng Command sau: 

Command: `timedatectl set-time '2019-05-07 16:00:00'`

- Changing the Time Zone
	- Hiển thị danh sách Time Zone: `timedatectl list-timezones`
	- Để thay đổi time zone: `timedatectl set-timezone time-zone`

### 2. Command date

- Hiển thị thời gian hiện tại: `date`

Mặc định date hiển thị local time. Để hiển thị time trong UTC thêm option --utc or –u.

Có thể thay đổi forrmat hiển thị bằng câu lệnh: date + “format”

|Control SEquence| Descrption|
|----|----|
|%H|The Hour in the HH format|
|%M|The minute in the MM format|
|%S|second|
|%d|day|
|%m|month|
|%Y|Year|
|%Z|Time Zone|
|%F|The full date in the YYYY-MM-DD format (for example, 2013-09-16). This option is equal to %Y-%m-%d.|
|%T|The full time in the HH:MM:SS format (for example, 17:30:24). This option is equal to %H:%M:%S|

VD: `date +”%Y-%m-%d %H:%M”`

- Changing the Current Time

Command: `date --set HH:MM:SS`

Set the system clock in UTC rum command with the `--utc` or `–u`

Command: `date --set HH:MM:SS --utc`

- Changing the Current Date

Command: `date --set YYYY-MM-DD`

Khi thay đổi date thì time về 00:00:00

Run the command `date --set YYYY-MM-DD HH:MM:SS`

### 3. Sử dụng `hwclock`

- Hiển thị thời gian hiện tại 

`hwclock`

- Thiết lập thời gian

`hwclock --set --date "dd mmm yyyy HH:MM"`
