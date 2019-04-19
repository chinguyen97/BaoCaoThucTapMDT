##  File System

### 1. Khái niệm
**File system** là cách thức cấp phát không gian lưu trữ cho file, quản lý các thuộc tính của file, cách tổ chức sắp xếp dữ liệu trên các thiết bị sao cho việc tìm kiếm, truy cập tới dữ liệu nhanh chóng và thuận tiện. 

- **Disk**: Thiết bị lưu trữ dữ liệu : /dev/sda, /dev/sdb
- **Partitions**:  là các phân vùng của disk 

- **Các loại file system**:
	- Hệ điều hành Linux hỗ trợ một số loại file system gốc dược cung cấp bởi nhà phát triển Linux: ext3, ext4, btrfs, XFS,.. 
	- Ngoài ra hệ điều hành Linux còn cung cấp việc triển khai các file system sử dũng trên các hệ điều hành khác. windows (ntfs, vfat), SGI (xfs) ,MacOS (hfs, hfs +)


- **EXT3**: 
	- Kích thước file tối đa: 2TB
	- Kích thước ổ đĩa tối đa: 32TB

- **Ext4**:
	- Ra đời năm 2006, là phiên bản phát triển nhất của ext, Bản này lưu giữ các ưu điểm của các ext trước đó và có thêm một số tính năng nổi bật.
	- Hỗ trợ volume có dung lượng tối đa 1 exbibyte (1 EiB=10^30 TB) và file có kích thước 16 tebityte (1TiB=10624TB)
	- Cải thiện iệu suất tập tin lớn và chống phân mảnh.
	- Không giới hạn thư mục con
	- Kiểm tra toàn vẹn dữ liệu(checksum)
	- Tính toán thời gian chuẩn đến (1 nano giây =10^-9 giây)
	- Hạn chế:  Công nghệ cũ

- **Btrfs** ( B-tree file system)
	- Sử dụng năm 2014. mục tiêu nhằm giải quyết các vấn đề pooling, snapshot, checksum và tích hợp thiết bị mở rộng. Btrfs dựa trên công nghệ hoàn toàn mới và cải tiến.
	- Tự kiểm tra và sửa lỗi cấu trúc file system
	- Chống phân mảnh dữ liệu
	- Kiểm tra và khắc phục lõi của dữ liệu bằng các bản dự phòng
	- Hỗ trợ cơ chế Cloning(kể cả tập tin), subvolume và snapshot 
	- Toàn bộ dữ liệu và những thay đổi đc backup đều lưu trong 1 task.

- XFS:
	- Năm giới thiệu 1994. Áp dụng vào hệ ddeieuf hành LInux năm 2001
	- Hạn chế phân mảnh
	- Kích thước file tối đa: 8EB
	- Kích thước đĩa tối đa: 8EB
	- Không thể chia nhỏ phân vùng XFS
	- Áp dụng cho các hệ thống Server lớn, ( Không hỗ trợ để lưu trữ thư mục root hay /boot trong hệ thống Linux)

### 2. Mount 

**Có 2 loại**: 
- Mount tự động thông qua fiel cấu hình /etc/fstab
- Mount thủ công

 Cú pháp: `mount -t <định dạng> <file thiết bị> <mount point>`
mount point: thư mục trống đã tồn taị ( thướng đc tạo trong /mnt)

**Cấu trúc file fstab**
Fstab (File system table) là một bảng lưu trữ thông tin về các thiết bị, mount point và các thiết lập của nó. Khi khởi động hệ thống Linux sẽ đọc thông tin trong file này và tiến hành tự động mount thiết bị. Vì file /etc/fstab được lưu dưới dạng Plaintext nên chúng ta có thể sửa nó dễ dàng. 

Cột 1: Tên thiết bị (UUID) `sudo blkid`
- Cột 2: mount point
- Cột 3: định dạng
- Cột 4: các tùy chọn
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
