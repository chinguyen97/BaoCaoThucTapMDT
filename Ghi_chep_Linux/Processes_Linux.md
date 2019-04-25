### Procces Linux
### 1. Phân loại tiến trình

#### a. Tiến trình Foreground trong Unix/Linux

Theo mặc định, mọi tiến trình mà bạn bắt đầu chạy là Foreground Process. Nó nhận input từ bàn phím và gửi output tới màn hình.

VD: Bạn nhập lệnh ls và kết quả trả ra các file và thư mục
Foreground Process kết quả của nó được hướng trực tiếp trên màn hình
Trong khi một chương trình đang chạy trong Foreground và cần một khoảng thời gian dài, chúng ta không thể chạy bất kỳ lệnh khác (bắt đầu một tiến trình khác) bởi vì dòng nhắc không có sẵn tới khi chương trình đang chạy kết thúc tiến trình và thoát ra.

#### b. Tiến trình Background trong Unix/Linux

Background Process chạy mà không được kết nối với bàn phím của bạn. 
Lợi thế của chạy một chương trình trong Background là bạn có thể chạy các lệnh khác; bạn không phải đợi tới khi nó kết thúc để bắt đầu một tiến trình mới!

Mỗi một tiến trình Unix có hai ID được gán cho nó: Process ID (pid) và Parent Process ID (ppid). Mỗi tiến trình trong hệ thống có một Parent Process (gốc).
### 2. Các câu lệnh liên quan 

### 2.1. top 
Liệt kê hệ thống hiện tại có các chương trình nào đang chạy

```
[root@localhost /]# top
top - 11:21:02 up  1:27,  2 users,  load average: 0.00, 0.01, 0.05
Tasks: 103 total,   1 running, 102 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :   995896 total,    60556 free,   134852 used,   800488 buff/cache
KiB Swap:  2621432 total,  2621432 free,        0 used.   669688 avail Mem 

   PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                
  7683 root      20   0  161984   2204   1556 R  0.7  0.2   0:00.17 top                    
     1 root      20   0  128016   4860   2460 S  0.0  0.5   0:05.27 systemd                
     2 root      20   0       0      0      0 S  0.0  0.0   0:00.03 kthreadd               
     3 root      20   0       0      0      0 S  0.0  0.0   0:01.32 ksoftirqd/0            
     5 root       0 -20       0      0      0 S  0.0  0.0   0:00.00 kworker/0:0H           
     7 root      rt   0       0      0      0 S  0.0  0.0   0:00.00 migration/0   
```
Dòng 1: Thời gian uptime (từ lúc khởi động), số người dùng thực tế đang hoạt động.
Dòng 2: Thống kê về số lượng tiến trì, Tổng số tiến trình (total), số tiến trình đang hoạt động, đang ngủ/chờ, đã dừng và số không thể dừng hẳn
Dòng 3-5: Thông tin CPU, RAM, bộ nhớ Swap.
Các dòng còn lại liệt kê chi tiết về các tiến trình như định danh (PID), người dùng (USER), độ ưu tiên (PR), dòng lệnh thực thi (command)...

`tp -b -n1 >/tmp/process.log` :  lưu lại danh sách tiến trình của lệnh top sang một tập tin .log

- Hoặc gửi một email chứa các thông tin đang có 

`top -b -n1 | mail -s 'Process snapshot' you@example.com`

### 2.2. ps Liệt kê các tiến trình
```
[root@localhost /]# ps
   PID TTY          TIME CMD
  7311 pts/0    00:00:00 su
  7315 pts/0    00:00:00 bash
  7685 pts/0    00:00:00 ps

```
Khác so với top
+ Chỉ hiện từ dòng 6 của lệnh top
+ top hiển thị 1 cách realtime các tiến trình thì ps chỉ hiện thị thông tin tại thời điểm khởi chạy lệnh.

**`ps -f`** full: Cung cấp nhiều thông tin hơn

```
[root@localhost /]# ps -f
UID         PID   PPID  C STIME TTY          TIME CMD
root       7311   7292  0 10:02 pts/0    00:00:00 su root
root       7315   7311  0 10:02 pts/0    00:00:00 bash
root       7687   7315  0 11:26 pts/0    00:00:00 ps -f
[root@localhost /]# 

```
|Cột|Miêu tả|
|---|---|
|UID|	ID người sử dụng mà tiến trình này thuộc sở hữu (người chạy nó).|
|PID|	Process ID.|
|PPID|	Process ID gốc (ID của tiến trình mà bắt đầu nó).|
|C|	CPU sử dụng của tiến trình.|
|STIME|	Thời gian bắt đầu tiến trình.|
|TTY|	Kiểu terminal liên kết với tiến trình.|
|TIME|	Thời gian CPU bị sử dụng bởi tiến trình.|
|CMD|	Lệnh mà bắt đầu tiến trình này.|

Các option 
-a	Chỉ thông tin về tất cả người sử dụng. ps -a =ps
-x	Chỉ thông tin về các tiến trình mà không có terminal.
-u	Chỉ thông tin thêm vào như chức năng -f.
-e	Hiển thị thông tin được mở rộng.
-U user xem process của các user khác
-l Thể hiện dưới dạng danh sách dài
```
[root@localhost /]# ps -l
F S   UID    PID   PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
4 S     0   7311   7292  0  80   0 - 47968 do_wai pts/0    00:00:00 su
4 S     0   7315   7311  0  80   0 - 28860 do_wai pts/0    00:00:00 bash
0 R     0   7688   7315  0  80   0 - 38309 -      pts/0    00:00:00 ps
```
```
[root@localhost /]# ps -aux
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        873  0.0  0.2  15824  2084 tty4     Ss+  07:50   0:00 /sbin/getty -8 38400 tty4
root        877  0.0  0.2  15824  2072 tty5     Ss+  07:50   0:00 /sbin/getty -8 38400 tty5
root        882  0.0  0.2  15824  2020 tty2     Ss+  07:50   0:00 /sbin/getty -8 38400 tty2
root        883  0.0  0.2  15824  2084 tty3     Ss+  07:50   0:00 /sbin/getty -8 38400 tty3
root        886  0.0  0.2  15824  2124 tty6     Ss+  07:50   0:00 /sbin/getty -8 38400 tty6
root       1023  0.0  0.3  78192  3528 tty1     Ss   07:50   0:00 /bin/login --    
root       1216  0.0  0.3  64536  3576 pts/0    S    07:52   0:00 su root
root       1217  0.0  0.3  21104  3744 pts/0    S    07:52   0:00 bash
root       1266  0.0  0.2  18452  2440 pts/0    R+   08:06   0:00 ps -u

```

Ý nghĩa các trường: 
|Trường|Mô tả|
|----|----|
|User/UID|Tên tiến trình|
|PID|ID của tiến trình|
|%CPU|%CPU sử dụng của tiên strinhf|
|%MEM|% bộ nhớ tiên strinhf sử dụng|
|SIZE|Kích thước bộ nhớ ảo tiến trình sử dụng|
|RSS|KÍch thước thực sự sử dụng bởi tiến trình|
|TTY|Vùng làm việc của tiến trình|
|STAT|Trạng thái của tiến trình|
|START|Thời gian hay ngày bắt đầu tiến trình|
|TIME|Tổng thời gian sử dụng CPU|
|COMMAND|Các lệnh được thực hiện|
|PRI|Mức ưu tiên của tiến trình|
|PPID|ID của tiến trình cha|
|WCHAN|Tên hàm nhân khi tiến trình ngủ được lấy từ file /boot/System.map|
|FLAGS|Số cờ được kết hợp với tiến trình|

- `ps -A`/`ps -e`: Xem tất cả các tiến trình của hệ thống
- `ps -u abc`: Xem tiến trình chạy bởi người dùng abc
- `ps -U root -u root -N` Xem mọi tiến trình của người dùng root

### 2.3: pstree
- pstree: Hiển thị tiến trình dưới dạng cây (ko hỗ trợ trên centos7)

### 2.4: Dừng tiến trình đang hoạt động

- Khi tiến trình đang chạy trong chế độ Foreground 
`Ctrl+c`

- Background
`kill PID`

- `pkill` & `killall`

Hai câu lệnh này cho phép bạn kill tiến trình bằng cách cung cấp tên của chúng:

- `renice` yêu cầu cung cấp PID của tiến trình

- `kill -9 PID`: ngừng thi hành tiến trình mà không bị các tiến trình khác can thiệp 

### 3. Tìm kiếm một tiến trình
VD: pgrep sshd
Kết quả sẽ cho chúng ta biết ID của chương trình firefox là gì.
VD : $ pgrep -u root sshd
ìm tiến trình của chương trình sshd do người dùng root thực hiện.
Hoặc: `ps aux | grep httpd ps aux | grep apache2 ps aux | grep  firefox`

### 4. Quản lý tiến trình bằng giao diện
2 công cụ atop và htop
cài đăt ubuntu 
# apt-get install htop

# apt-get install atop 

Để hiển thị gõ htop / atop


slof 

***Tài liệu tham khảo:***
https://cuongquach.com/linux-huong-dan-su-dung-chuong-trinh-lenh-lsof-tren-linux.html
