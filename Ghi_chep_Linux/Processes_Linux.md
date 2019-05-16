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

#### 2.1.1. Dòng 1: Thời gian uptime (từ lúc khởi động), số người dùng thực tế đang hoạt động, load average.

Có thể sử dụng lệnh `uptime` để hiển thị 3 thông số này. 
```
chi@ubuntus:~$ uptime
 11:55:53 up  3:44,  1 user,  load average: 0.01, 0.03, 0.05
```
**Load average** là các chỉ số tải trung bình của CPU trong các khoảng thời gian 1 phút, 5 phút và 15 phút, và những chỉ số này càng thấp càng tốt, càng cao thì chứng tỏ CPU của bạn đang overload

  + Trường hợp: single-core CPU
Các chỉ số nhỏ hơn 1 tức là hệ thống đang hoạt động trơn tru. =1 nghĩa là VPS hoạt động bình thường. >1. hệ thống xử lý đang bị kẹt. 
Các nhà quản trị system thường lấy ở mức 0.70 làm chuẩn:Nếu bạn thấy chỉ số tải CPU trên mức 0.70 thì chúng ta cần chú ý. Nếu chỉ số này đạt trên mức 1.00 thì bạn phải lập tức tìm ra nguyên nhân, nhưng với khoảng thời gian trung bình 1 phút thì có thể chấp nhận, nếu nó ở chỉ số thứ 2 là 5 phút thì bạn sẽ ngủ không ngon đâu đấy.Nếu chỉ số tải CPU trên 5.00, bạn đang phải đối mặt với vấn đề nghiêm trọng. Đừng để VPS bạn tới mức này mới bắt đầu đi tìm nguyên nhân nhé.
  + Trường hợp Nhiều core: 
Tương ứng mỗi core sẽ đảm nhận 1.. chỉ số
VD CPU i5: 4.00
core i7 có 8 core: 8.00

#### 2.1.2. Dòng 2: Thống kê về số lượng tiến trì, Tổng số tiến trình (total), số tiến trình đang hoạt động, đang ngủ/chờ, đã dừng và số không thể dừng hẳn

- Tiến trình sleep
Tiến trình ngủ bắt đầu bằng chữ S/D trong cột STAT
Tiến trình ngủ ( chờ để 1 sự kiện hoàn thành)
Lọc tiến trình đang ngủ : `ps aux | grep S/D`

- Tiến trình zombie

Lọc tiến trình zombie 
`ps aux | grep Z`

Zombie thực chất là một phần còn sót lại của một tiến trình đã ngừng hoạt động nhưng chưa được xử lý sạch. Những chương trình sau khi thoát để lại tiến trình Zombie thì điều đó đồng nghĩa với việc chương trình đó được lập trình không tốt.

Muốn hiểu chính xác quá trình này, bạn cần có một chút hiểu biết về cách hoạt động của các tiến trình trong HĐH Linux. Một khái niệm bạn gần biết nữa là tiến trình cha mẹ (parent process) là tiến trình khi thực thi tạo ra các tiến trình khác.
Trong Linux, khi một tiến trình kết thúc, HĐH sẽ không xóa nó khỏi bộ nhớ ngay lập tức. Thay vào đó, Linux vẫn giữ lại mô tả tiến trình (process discriptor) trong bộ nhớ (Mô tả tiến trình chỉ chiếm một lượng nhỏ bộ nhớ). Lúc này, trạng thái của tiến trình sẽ là EXIT_ZOMBIE và “cha mẹ” của tiến trình đó được thông báo rằng tiến trình con đã “chết” với tín hiệu tên là SIGCHLD. Tiến trình cha mẹ sau đó có nghĩa vụ thực thi chức năng wait() với nhiệm vụ đọc trạng thái và thông tin của tiến trình đã chết đó. Sau khi chức năng wait() được gọi, tiến trình Zombie lúc này sẽ được xóa hoàn toàn khỏi bộ nhớ.
Quá trình này thường diễn ra khá nhanh, vì thế bạn sẽ không thể nhìn thấy những tiến trình thây ma. Tuy nhiên nếu tiến trình cha mẹ được lập trình cẩu thả và không bao giờ thực hiện chức năng wait(), tiến trình thây mà sẽ nằm lại trong bộ nhớ đến khi hệ thống được khởi động lại.

**Nguy hiểm của tiến trình zombie**

- Tiến trình Zombie hầu như không sử dụng tài nguyên hệ thống chỉ chiếm một chút dung lượng để lưu mô tả tiến trình. Mỗi tiến trình dưc[j gán 1 PID tuy zombie adx chết nhưng vẫ đc coi là 1 tiên strinfh và chiếm 1 PID. Linux có số lượng PID hữu hạn ( Bản 32bit - có 32767 PID). Nếu tiến trình Zombie dọng lại quá nhiều , PID bị chiếm hết thfi sẽ không theher bắt đầu các tiên strinfh khác. Tuy nheien nếu chỉ có 1 vài tiến trình sẽ ko gây hại cho máy tính của bạn. 

**Cách dọn dẹp tiến trình Zombie** 
Tiến trình Zombie là tiến trình đã chết nên về bản chất bạn không thể kill nó thêm 1 lấn nữa. Bạn cũng không cần dọn dẹp tiên strinfh thây ma trừ khi chúng tràn ra bộ nhớ. 
Cách thứ nhất là gửi tín hiệu SIGCHLD đến tiến trình cha mẹ. Tín hiệu này sẽ ra lệnh cho tiến trình cha mẹ thực hiện chức năng wait() và dọn sạch những “đứa con” đó. Gửi tín hiệu với lệnh kill, thay thế pid bằng ID của tiến trình cha mẹ:

`kill -s SIGCHLD pid`

Tuy nhiên, nếu các tiến trình cha mẹ không được lập trình kỹ lưỡng, nó thậm chí sẽ lờ đi tín hiệu SIGCHLD và câu lệnh trên là vô ích, bạn sẽ phải tự mình “kill” tiến trình cha mẹ. Khi một tiến trình tạo ra tiến trình thây ma bị giết, tiến trình với tên init sẽ thừa kế lại những tiến trình thây ma và trở thành tiến trình cha mẹ mới (init là tiến trình đầu tiên khởi động khi Linux khởi động, có PID là 1), sau đó init sẽ thực hiện định kỳ chức năng wait() để dọn dẹp. Bạn có thể khởi động lại tiến trình cha mẹ sau khi tắt chúng đi.

#### 2.1.3. Dòng 3
Dòng thứ 3 hiển thị % sử dụng CPU dành cho acc stacs vụ khác nhau, bao gồm % CPU từ user (us), system (sy), low-priority processes (nice time, hoặc ni), idle time (id) thời gian CPU rảnh , wait for I/O processes (wa) Thời gian CPU dành để chờ I/O hoàn thành, time handling hardware interruptions (hi) Thời gian dành cho ngăt sx]r lý phần cứng, time handling software interruptions (si) Thời gian dành cho ngắt xử lý phần mềm, stolen time from the virtual machine (st) Trong môi trường ảo hóa, một phần tài nguyên CPU được cung cấp cho mỗi máy ảo (VM). HĐH phát hiện khi nào có việc phải làm, nhưng nó không thể thực hiện chúng vì CPU đang bận trên một số VM khác. Lượng thời gian bị mất theo cách này là thời gian ăn cắp thời gian, được hiển thị là st.
#### 2.1.4. 

- Dòng thứ 4 hiển thị tình trạng sử dụng Memory theo kilobytes.
- Dòng 5 là Swap theo kilobytes.
- Các dòng còn lại liệt kê chi tiết về các tiến trình như định danh (PID), người dùng (USER), độ ưu tiên (PR), dòng lệnh thực thi (command)...

|Comments|Mô tả|
|---|---|
|PID| ID process|
|user|user|
|PR|Hiển thị mức độ ưu tiên lập lịch của 1 uy trình theo quan điểm của kernel|
|NI|nice Giá trị `nice` của 1 tiến trình|
|VIRT| Tỏng bộ nhớ tiêu thụ bởi 1 quá trình|
|RES|Là bộ nhớ được tiêu thụ bởi tiến trình RAM|
|SHR| Số lượng bộ nhớ chia sẻ với các quy trình khác|
|S| STATE- Trạng thái của 1 tiến trình|
|%CPU|% chiếm dụng dug lượng CPU|
|%MEM| % Tổng RAM sẵn có|
|TIME +|Tổng thời gian CPU được sử dụng bởi lệnh|
|COMMAND|Hiện thị tên accs quy trình|

#### 2.1.5. Một số tác vụ khác của lệnh top

- Top đi kèm gói tin `procps-ng`
```
[chinguyen@CentOS7 ~]$ top -v
     procps-ng version 3.3.10
```

- Lưu lại danh sách tiến trình của lệnh top sang một tập tin .log: `tp -b -n1 >/tmp/process.log` 

- Hoặc gửi một email chứa các thông tin đang có 

`top -b -n1 | mail -s 'Process snapshot' you@example.com`

- Sắp xếp danh sách các tiến trình: Chạy lệnh top sau đó ấn phím
  - **M** to sort by memory usage
  - **P** to sort by CPU usage
  - **N** to sort by process ID
  - **T** to sort by the running time
Mặc định nó sẽ sắp xêp stheo thứ tự giảm dần. Để sắp xếp theo thứ tự tăng dần ấn **R**
- Show full paths
Chạy lệnh top và ấn `c` . ấn `c` để quay trở lại mặc định

- Hiện thị tiến trình theo phân cấp cha con. Ấn phím H chỉnh về mặc định ấn lại H

- Thay đổi giao diện hiển thị ấn 't' và `m`

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

### 2.3: Hiển thị tiến trình dạng cây

- Với ubuntu: Có thể sử sụng 1 trong các câu lệnh 

`pstree` or `ps -ejH` /  `ps -axjf`

- CentOS7: Không hỗ trợ lệnh `pstree` 
Nên phải cài đặt gói `psmic`

`yum install psmic`

Cũng sử dụng được 2 câu lệnh: `ps -ejH` or `ps -axjf`

### 2.4: Dừng tiến trình đang hoạt động

- Khi tiến trình đang chạy trong chế độ Foreground 
`Ctrl+c`

- Background
`kill PID`

- `pkill` & `killall`

Hai câu lệnh này cho phép bạn kill tiến trình bằng cách cung cấp tên của chúng:
CentOS7 ko hỗ trợ `killall` nên cần phải tải gói `psmisc`;

`yum install psmisc`

- `renice` yêu cầu cung cấp PID của tiến trình


- `kill -[POSIX signal] PID`

Để liệt kê danh sách các tín hiệu POSIX `kill -l`

```
[chinguyen@CentOS7 ~]$ kill -l
 1) SIGHUP      2) SIGINT      3) SIGQUIT     4) SIGILL      5) SIGTRAP
 6) SIGABRT     7) SIGBUS      8) SIGFPE      9) SIGKILL    10) SIGUSR1
11) SIGSEGV    12) SIGUSR2    13) SIGPIPE    14) SIGALRM    15) SIGTERM
16) SIGSTKFLT  17) SIGCHLD    18) SIGCONT    19) SIGSTOP    20) SIGTSTP
21) SIGTTIN    22) SIGTTOU    23) SIGURG     24) SIGXCPU    25) SIGXFSZ
26) SIGVTALRM  27) SIGPROF    28) SIGWINCH   29) SIGIO 30) SIGPWR
31) SIGSYS     34) SIGRTMIN   35) SIGRTMIN+1 36) SIGRTMIN+2 37) SIGRTMIN+3
38) SIGRTMIN+4 39) SIGRTMIN+5 40) SIGRTMIN+6 41) SIGRTMIN+7 42) SIGRTMIN+8
43) SIGRTMIN+9 44) SIGRTMIN+10     45) SIGRTMIN+11     46) SIGRTMIN+12     47) SIGRTMIN+13
48) SIGRTMIN+14     49) SIGRTMIN+15     50) SIGRTMAX-14     51) SIGRTMAX-13     52) SIGRTMAX-12
53) SIGRTMAX-11     54) SIGRTMAX-10     55) SIGRTMAX-9 56) SIGRTMAX-8 57) SIGRTMAX-7
58) SIGRTMAX-6 59) SIGRTMAX-5 60) SIGRTMAX-4 61) SIGRTMAX-3 62) SIGRTMAX-2
63) SIGRTMAX-1 64) SIGRTMAX   
```
Thông tin các tín hiệu có thể xem 
[tại đây](https://en.wikipedia.org/wiki/Signal_(IPC)

`kill -9`: Gửi tín hiệu SIGKILL đến 1 tiến trình để nó chấm dứt ngay lập tức ( Trừ các tiens trình zombie, init process,...)

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
 

***Tài liệu tham khảo:***
[1]https://cuongquach.com/linux-huong-dan-su-dung-chuong-trinh-lenh-lsof-tren-linux.html

[2]https://www.booleanworld.com/guide-linux-top-command/