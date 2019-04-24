##  File System

### 1. Khái niệm
**File system** là cách thức cấp phát không gian lưu trữ cho file, quản lý các thuộc tính của file, cách tổ chức sắp xếp dữ liệu trên các thiết bị sao cho việc tìm kiếm, truy cập tới dữ liệu nhanh chóng và thuận tiện. 

- **Disk**: Thiết bị lưu trữ dữ liệu : /dev/sda, /dev/sdb
- **Partitions**:  là các phân vùng của disk 
Kiểm tra các parttion: cat /proc/partitions

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




