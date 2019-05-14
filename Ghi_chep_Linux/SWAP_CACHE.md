#### 

### 1. SWAP 

#### 1.1. Giới thiệu 
SWAP - Hay bộ nhớ ảo ( RAM ảo) được lấy từ ổ cứng. 
Nếu không có SWAP, khi RAM hết thì linux sẽ tự động ngắt kết nối và không thể truy cập và database.
Khi có bộ nhớ SWAP, khi RAM hết thì hệ thống server sẽ tự động phân phối hợp lý, giúp duy trì hoạt động liên túc. 

Lưu ý: SWAP là 1 vùng của ổ cứng nên tốc độ xử lý chậm hơn RAM vật lý. Ko thể coi swap là phương pháp thay tehes hoàn toàn cho RAM vật lý được. 

Kích thước SWAP khuyến nghị = kích thước RAM hoặc 1/2 RAM

#### 1.2. Cách khởi tạo 
- Cách kiểm tra Swap trước khi tiến hành tạo fiel swap cần kiểm tra hệ thống đã kích hoạt SWAP chưa bằng câu lệnh: 
`swapon -s`
- Kiểm tra dung lượng ổ cứng trống: Do SWAP lấy dung lượng từ ổ cứng nên cầ kiểm tra:
`df -h`
- Cách tạo SWAP. Sử dụng lệnh **dd**.

Ví dụ ở đây tạo ra SWAP 1GB(1024k), lấy dung lượng từ /dev/sdb1
```
sudo dd if=/dev/sdb1 of=/swapfile bs=1024 count=1024k
```
Tạo 512MB SwapFile (1024x512MB=524588 block size)
```
sudo dd if=/dev/sdb1 of=/swapfile bs=1024 count=524288`
```

Hoặc `sudo fallocate -l 512m /swapfile`
(Lệnh này sẽ tạo file swapfile có kích thước 512M tại /. Để tạo swap 2Gb thay 512m = 2G)

- Tạo phân vùng SWAP bằng câu lệnh 

`mkswap /swapfile`

- Kích hoạt swap 

`swapon /swapfile`

- Kiểm tra lại 

`swapon -s`


- Thiết lệp swap tự đông đươc kích hoạt khi reboot, khởi động lại. Bằng cách sửa đổi file `/etc/fstab`

Ví dụ: Thêm dòng

`/dev/sda1 /swapfile swap defaults 0 0`

- Muốn tắt swap 

`swapoff /swapfile` 

- Xóa fie swapfile 

**Xóa bộ nhớ swap**
`swapoff -a && swapon -a`

#### 1.3. Thiết lập Swappiness 

Tham số Swappiness sẽ quyết định khi nào các tài nguyên và dữ liệu được lưu giữ trong bộ nhớ RAM sẽ được di chuyển đến không gian Swap.

- Swappiness có giá trị từ 0-100.Swappiness có giá trị càng lớn thì hệ thống sẽ sử dụng Swap càng sớm càng tốt. Swappiness có giá trị càng nhỏ thì hệ thống sẽ sử dụng Swap càng chậm càng tốt.
	+ swappiness = 0: swap chỉ được dùng khi RAM được sử dụng hết.
	+ swappiness = 10: swap được sử dụng khi RAM còn 10%.
	+ swappiness = 100: swap được ưu tiên như là RAM.
 
- Kiểm tra giá trị swappiness `cat /proc/sys/vm/swappiness` 

- Thay đổi gía trị của Swappiness `sudo sysctl vm.swappiness=10`

Tuy nhiên việc thay đổi này không có giá trị trong các lần khởi động tiếp theo. 

- Để thiết lập giá trị này vĩnh viễn edit file `/etc/sysctl.conf`

Tìm đến dòng `wm.swappines` thay bằng `wm.swappiness=10`

Lưu file và khởi động lại máy. 

### 2. Cache
#### 2.1. Giới thiệu

Bộ nhớ cache là vùng lưu trữ tạm thời của một thiết bị, giúp giữ lại một số loại dữ liệu nhất định. Về cơ bản đây là một khu vực lưu trữ dữ liệu hoặc các quy trình được sử dụng thường xuyên để truy cập nhanh hơn trong tương lai.

Mục đích của việc này là tiết kiệm thời gian, tăng tốc độ hoạt động của thiết bị và giảm lượng dữ liệu cần xử lý trong quá trình sử dụng.

Linux sẽ “mượn” một phần RAM không sử dụng cho việc làm caching disk. Điều này bạn có thể hiểu với ví dụ này: bạn có một file, bạn chỉ cần đọc nó từ disk một lần và Linux sẽ giữ file đó của bạn trên RAM cho đến khi không cần nó nữa. Như vậy với việc giữ trên RAM thì file đó sẽ được truy cập nhanh hơn rất nhiều.

#### 2.2. Các câu lệnh 
Xem thông thin bộ nhớ cache
- lscpu (tất cả thông tin bộ nhớ)
- Hoặc: getconf -a | grep CACHE

- **`free -m`**: Hiển thị thông tin bộ nhớ
	- total: Tổng dung lượng RAM, Không bao gồm không bao gồm khoảng 300-500MB hệ thống chiếm dụng cố định khi khởi động hệthống
	- total = used + free. Used = memory in use by the OS; Free = memory not in use
	- shared / buffers / cached: This shows memory usage for specific purposes, these values are included in the value for used
```
[chinguyen@localhost ~]$ free -m
          total        used        free      shared  buff/cache   available
Mem:       972         121         713           7         137         692
Swap:      2047           0        2047
```

Hệ thống có tổng cộng 972M RAM, Thực tế sử dụng 121MB, Còn trống 713MB và 692MB sử dụng cho cache. SWap chưa dùng đến. Điều quan tâm là lượng RAM thực tế mà các ứng dụng có thể sử dụng: 692MB.

Đáng chú ý là: Avaiable memory hoặc free của -/+buffers/cache tiến đến 0 và Mức sử dụng swap tăng
```
 chi@ubuntu:/$ free -m
             total       used       free     shared    buffers     cached
Mem:           975        164        811          0         14         55
-/+ buffers/cache:         93        881
Swap:         1019          0       1019
```
Hệ thống có tổng cộng 975MB, đã sử dụng 193MB trống 881MB

#### 2.3. Xóa bộ nhớ Cache

### a. Clear PageCache only.

`sync; echo 1 > /proc/sys/vm/drop_caches`

Page cache là thông tin nằm trong cột cache khi bạn dùng free command để xem. Bất cứ khi có sự ghi data nào từ memory xuống disk thì data đó đều nằm luôn trong cache vì xác suất data vừa được ghi sẽ được đọc lại là khá cao.

### b. Clear dentries and inodes.

`sync; echo 2 > /proc/sys/vm/drop_caches`

Dentries là các component của một path + file name, ví dụ file /usr/bin/test sẽ tạo ra 4 dentries: /, usr, bin và test.

### c. Clear PageCache, dentries and inodes.
`sync; echo 3 > /proc/sys/vm/drop_caches`

";" Dấu tách lệnh, chạy theo tuần tự. Shell chờ lệnh trước kết thúc sẽ thực hiện lệnh tiếp theo. Vieech ghi vào drop_cache sẽ xóa bộ nhớ cache mà ko ảnh hưởng đén chương trình nào. lệnh echo thực hiện công việc ghi vào lệnh.
Nếu phải xáo bộ đĩa đệm, Lệnh đầu tiên chỉ xáo PaggeCache anh toàn nhất cho các doanh nghiệp. Ko nên sử dụng tùy chọn 3.

Linux được thiết kế theo cách nó nhìn vào bộ đệm đĩa trước khi nhìn vào đĩa. Nếu nó tìm thấy tài nguyên trong bộ đệm, thì yêu cầu không đến được đĩa. Nếu chúng ta xóa bộ đệm, bộ đệm đĩa sẽ ít hữu ích hơn vì HĐH sẽ tìm tài nguyên trên đĩa.
Ngoài ra, nó cũng sẽ làm chậm hệ thống trong vài giây trong khi bộ đệm được dọn sạch và mọi tài nguyên mà HĐH yêu cầu sẽ được tải lại trong bộ đệm đĩa.

### Lệnh alias: 
Hiểu đơn giản lệnh alias như 1 cách đặt tên khác cho câu lệnh:

Mặc định các lệnh viết tắt được lưu trong file ẩn ~./bashrc hoặc ~/.bash_profile 

Hiện danh sách alias : Trên trên terminal gõ `alias` 

Muốn thêm 1 alias mở file `./bashrc`. Thêm dòng định nghĩa alias

Cú pháp: `alisa tên_alisa='command'`

Lưu và cập nhật thay đổi: 

`source ~./bashrc`