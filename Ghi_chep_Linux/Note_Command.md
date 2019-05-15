#### Note Command 

1. Sử dụng lệnh trước đó vừa sử dụng
`!!`
Hoặc ấn phím `pgup` 
Hoặc ấn phím đi lên
```
[chinguyen@CentOS7 chichi]$ ls
777  folder
[chinguyen@CentOS7 chichi]$ !!
ls
777  folder

```
2. Sử dụng lệnh gần nhất đã sử dụng bắt đầu bằng 1 chữ cái
`!(text)`
```
[chinguyen@CentOS7 ~]$ !p
ps
   PID TTY          TIME CMD
  7280 pts/0    00:00:00 bash
  7304 pts/0    00:00:00 ps
```
3. Copy file
`cp file1 file2`

4. Commad `cd`
- `cd` Hoặc `cd ~`: Di chuyển về thư mục home
- `cd -` Chuyển đến thư mục vừa thoát
- `cd ..` : Chuyển đến thư mục cha của thư mục hiện tại

5. copy thư mục này thành thư mục khác/ Copy thư mục này vào thư mục khác

`cd -r <directory1> <directory2>`

6. Hiển thị thời gian máy tính
`date`
hoặc `timedatectl`
hoặc `hwclock`

7. Command `dmidecode`
Hiển thị thông tin hệ thống

- `dmidecode -t 0` Hiển thị thông tin BIOS
- `dmidecode -t 4` Hiển thị thông tin CPU
8. Tìm kiếm các gói đã cài đặt liên quan đến `zip`

```
[root@CentOS7 ~]# yum list installed | grep zip
Repository 'REPO_OFF' is missing name in configuration, using id
bzip2-libs.x86_64                    1.0.6-13.el7                    @anaconda  
gzip.x86_64                          1.5-10.el7                      @anaconda  
```

9. Ước tính không gian đĩa, tệp `du -bh (đường dẫn)`
```
[root@CentOS7 ~]# du -bh /root
6	/root/.pki/nssdb
25	/root/.pki
37K	/root
```

10. In ra biến môi trường
```
[root@CentOS7 ~]# x=11
[root@CentOS7 ~]# echo $x
11
```
11. Hiển thị biến môi trường
`env`

hoặc `printenv`
12. 

/27
/30

14. Tìm kiếm 1 chuỗi trong file
`grep <string> <filename>`

15. Số giây hệ điều hành chạy
`grep btim /proc/stat`

16. Hiển thị thông tin wireless interface/ wireless network (ubuntu)
`iwconfig`

17. Hiển thị khoảng thời gian shutdown gần đây nhất

`last -x | grep shutdown |heat -1`

18. Logout khỏi user hiện tại

`logout`

19. Hiển thị tất cả các lệnh sãn có

`ls /usr/bin`

20. Hiển thị thêm thông tin về network (ubuntu)

`lshw -C network` 

21. Hiển thị các modules hiện đang load trong kelnel (ubuntu)

`lsmod`

22. Show thông tin phần cứng âm thanh, video, network (ubuntu)

`lspci -nv | less`

23. Hiển thị thông tin USB bus trong hệ thống và các thiết bị kết nối đến nó. 

`lsusb`

24. Show bảng định tuyến (ubuntu)

`netstat -rn` Hoặc `route`

Hoặc `ip r` cho cả ubuntu và centOS7

25. Shutdown now

`shutdown -h now`

26. Restart now

`shutdown -r now`

27. In ra tên của terminal đang sử dụng

`tty`

28. Mô tả command

`whatis <command`

29. Vị trí 1 command trong hệ thống

`whereis <command>`

30. Trả về đường dẫn của 1 ứng dụng

`which <command>`

31. In ra user đang truy cập  vào máy

`who`

32. In ra tên mà bạn đang nhập vào máy

`whoami`

33. In ra thông tin hiệu suất

`cat /proc/uptime`

34. Hiển thị trạng thái của file

`stat filename`

35. In ra danh sách 10 người đăng nhập cuối cùng vào máy. 

`last -n 10`

36. ....


**Link tham khảo:**

https://github.com/nhanhoadocs/thuctapsinh/blob/master/linux_command/101_commands_linux.md