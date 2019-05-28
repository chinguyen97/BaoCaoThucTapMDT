
### System Infor 

### 1. Command `uname`

|Command| Mô tả|
|---|---|
|`uname -a`| Hiện thị tất cả thông tin hệ thống|
|`uname`/`uname -s`|Tên kernel|
|`uname -n`| Tên hostname|
|`uname -r`| Số bản phát hành |
|`uname -v`| Số phiên bản phst hành|
|`uname -m`| Kiến trúc phần cứng|
|`uname -p`| Loại bộ vi xử lý|
|`uname -o`| Thông tin Hệ điều hành|
|`uname -i`| Nền tảng phần cứng|

Ví dụ: 
```
chi@ubuntu:~$ uname -r
4.2.0-27-generic
chi@ubuntu:~$ uname -v
#32~14.04.1-Ubuntu SMP Fri Jan 22 15:32:26 UTC 2016
```

```
[chinguyen@CentOS7 ~]$ uname -m
x86_64
[chinguyen@CentOS7 ~]$ uname -p
x86_64
[chinguyen@CentOS7 ~]$ uname -o
GNU/Linux
[chinguyen@CentOS7 ~]$ uname -a
Linux CentOS7 3.10.0-957.el7.x86_64 #1 SMP Thu Nov 8 23:39:32 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

Kiến trúc phần cứng: Đầu ra x86_64 : Đang sử dụng kiến trúc 64 bit. Đầu ra i686 có nghĩa là đang sử dụng hệ thống 32 bit. 


- `cat /proc/version` Hiển thị phiên bản linux

```
chi@ubuntu1:~$ cat /proc/version
Linux version 4.2.0-27-generic (buildd@lcy01-23) (gcc version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) ) #32~14.04.1-Ubuntu SMP Fri Jan 22 15:32:26 UTC 2016
```
Hoặc dùng câu lệnh: `dmesg | grep "Linux version"`

Hoặc xem file `cat /etc/*relesae`

- lsb_release : Hiển thị thông tin Distro (Ubuntu)

```
chi@ubuntu1:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 14.04.4 LTS
Release:	14.04
Codename:	trusty
chi@ubuntu1:~$ 
```
### 2. Thông tin CPU, RAM..
### 2.1. Thông tin CPU

- Thông tin CPU: `lscpu`

```
chi@ubuntu1:~$ lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                1
On-line CPU(s) list:   0
Thread(s) per core:    1
Core(s) per socket:    1
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 61
Stepping:              4
CPU MHz:               2196.824
BogoMIPS:              4393.64
Hypervisor vendor:     VMware
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              3072K
NUMA node0 CPU(s):     0
chi@ubuntu1:~$ 
```
Thông tin CPU còn được hiển thị chi tiết trong file: `/Proc/ cpuinfo`

### 2.2. Thông tin ổ cứng, phân vùng, ổ đĩa flash 

- `lsblk` :Hiển thị thông tin về các ổ cứng, phân vùng, ổ đĩa flash. 

Sử dụng tùy chọn -a để hiển thị chi tiết hơn.

```
[chinguyen@CentOS7 /]$ lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0   20G  0 disk 
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   19G  0 part 
  ├─centos-root 253:0    0   17G  0 lvm  /
  └─centos-swap 253:1    0    2G  0 lvm  [SWAP]
sr0              11:0    1  918M  0 rom  
```

- Thông tin về thiết bị USB : `lsusb` (ubuntu) 

Option -v để hiển thị chi tiết.

```
chi@ubuntu1:/proc$ lsusb 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 003: ID 0e0f:0002 VMware, Inc. Virtual USB Hub
Bus 002 Device 002: ID 0e0f:0003 VMware, Inc. Virtual Mouse
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
```
-	Xem RAM: `cat /proc/meminfo` hoặc `free`

-	Xem HDD: `df –h` : Phân vùng

Hoặc `cat /proc/partitions`

- Xem thông tin các thiết bị khác. 

`lspci`: Thông tin thiết bị cpi

`lsscsi`: Thông tin thiết bị SCSI

`hdparm /dev/sda/` Thông tin về thiết bị SATA

top : kích thước bộ nhớ

### 3. Command lshw

- Install: yum install lshw
- Display full information hardware: `sudo lshw`
- Display information in short: `sudo lshw -short`
- Display only memory information: `lshw -short -class memory`
- Display processor information: `sudo lshw -class processor`
- Disk drives: `sudo lshw -short -class disk`
- Network adapter information: `sudo lshw -class network`
- Display address details with businfo (pci, usb, scsi and ide devices): `sudo lshw -businfo`

### 4. Thay đổi hostname

- Xem tên máy
`hostname`

- Thay đổi tên máy tạm thời ( Khi reboot sẽ trở về tên cũ)
`hostname [new_hostname]`
- Thay đổi vĩnh viễn
	+ Cách 1:  Đối với Ubuntu phiên bản 14.04 trở lên, bạn chỉ cần thay đổi hostname bằng 1 câu lệnh duy nhất: `hostnamectl set-hostname hostname`  
	+ Cách 2: Chỉnh sửa file `/etc/hostname`
Sau đó khới động lại dịch vụ
`service hostname restart`

hoặc khởi đôngk lại máy
`reboot`
 
Môi trường: UbuntuServer 14.04 . CentOS7