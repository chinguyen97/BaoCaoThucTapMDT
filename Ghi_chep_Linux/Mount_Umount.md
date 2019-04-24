#### Mount, Umount 

Mount là hành động gắn 1 thiết bị lưu trữ đến 1 vị trí trong cây thư mục. 

### 1. Phân loại

**Có 2 loại**: 
- Mount tự động thông qua file cấu hình /etc/fstab
+ Tính chất cố định, tắt máy mở lên không bị mất, khởi động lại hệ thống.
- Mount thủ công, 
+ Có tính chất tạm thời, sẽ bị mất khi khởi động lại máy

Cú pháp: `mount -t <định dạng> <file thiết bị> <mount point>`

mount point: thư mục trống đã tồn taị ( thướng đc tạo trong /mnt)

**Umount** : Khi xong việc có nhu cầu gỡ thiết bị ra bạn dùng lệnh

`umount <file thiet_bi>`

Hoặc: `umount mount-point`


### 2. Cấu trúc file fstab
Fstab (File system table) là một bảng lưu trữ thông tin về các thiết bị, mount point và các thiết lập của nó. Khi khởi động hệ thống Linux sẽ đọc thông tin trong file này và tiến hành tự động mount thiết bị. Vì file /etc/fstab được lưu dưới dạng Plaintext nên chúng ta có thể sửa nó dễ dàng. 

- Cột 1: Tên thiết bị (UUID) `sudo blkid`
- Cột 2: Mount point
- Cột 3: Định dạng: ext2, ext3, ext4, swap,.....
- Cột 4: Mount option 
	- auto: tự động mount thiết bị khi máy tính khởi động
	- noauto: Bạn phải tự chạy lệnh mount sau khi khởi động hệ thống.
	- user: cho phép người dùng thông thường được quyền mount.
	- nouser: chỉ có người dùng root mới có quyền mount.
	- exec: cho phép chạy các file nhị phân (binary) trên thiết bị.
	- noexec: không cho phép chạy các file binary trên thiết bị.
	- ro (read-only): chỉ cho phép quyền đọc trên thiết bị.
	- rw (read-write): cho phép quyền đọc/ghi trên thiết bị.
	- sync: thao tác nhập xuất (I/O) trên filesystem được đồng bộ hóa.
	- async: thao tác nhập xuất (I/O) trên filesystem diễn ra không đồng bộ.
	- defaults: tương đương với tập các tùy chọn rw, suid, dev, exec, auto, nouser, async
- Cột 5: là tùy chọn cho chương trình sao lưu filesystem. Điền 0: bỏ qua việc sao lưu, 1: thực hiện sao lưu.
- Cột 6: là tùy chọn cho chương trình fsck dò lỗi trên filesystem. Điền 0: bỏ qua việc kiểm tra, 1: thực hiện kiểm tra.
 Ví dụ: 
 `/dev/sdd1 /home/chi/data1 ext4 rw 0 2`

### 3. Các bước thực hiện: 

- B1: Tạo Hard Disk
- B2: Chia partition : `fdisk /dev/sdd`
 
 `#cat /proc/partiition`

- B3: Dùng lệnh mkfs để format 

 `#mkfs -t ext4 /dev/sdd1`
- B4: Tạo monut point

 `mkdir /home/chi/data1`
- B5: Mount
 C1: Mount thủ công
 `#mount -t ext4 /dev/sdd1 /home/chi/data1`

 C2: Edit file /etc/fstab
`/dev/sdd1 /home/chi/data1 ext4 rw  0 2`

Kiểm tra tất các mount pint trong máy
`df -l`
Liệt kê các mount được kết nối trong máy

`# mount`

Hoặc: `# mount -a` : Độc hết các dòng trong file và tạo kết nối lại
