## Hướng dẫn cài đặt Ubuntu Server trên VMware 
### Chuẩn bị:
 Phần mềm Vmware, file iso phiên bản Ubuntu server muốn cài đặt.
### Các bước thực hiện
- Mở Vmware chọn Create a New Virtual Machine để tạo 1 máy ảo mới

<img src="image/25.png">

- Lựa chọn loại cấu hình

	- Option **Typical(recommendede)**: Tạo theo định dạng măc định của máy
	- Option **Custom(advanced)**: Các tùy chọn do người dùng cài đặt
	- Máy ảo được cài đặt với một số tùy chọn mở rộng khác

Ở đây mình chọn **Custom**. Nhấn **Next** để tiếp tục.

<img src="image/26.png">

- Tương thích phần cứng: Ở đây phiên bản Umware mình cài là 12.0. Nhấn **Next**

<img src="image/27.png">

- Cài đặt Hệ điều hành

	- Installer disc: Sử dụng ổ đĩa để cài đặt
	- Installer disc image file(isso): cài băng file iso
	- I will     Cài đặt hệ điều hành sau. Máy ảo sẽ được tạo với đĩa cứng trống

<img src="image/28.png">
	

<img src="image/29.png">

- Đặt tên máy ảo và vị trí lưu trữ máy ảo. Muốn thay đổi vị trí nhấn **Browse** chọn vị trí muốn lưu.

<img src="image/30.png">

- Cấu hình bộ vi xử lý (CPU)
	- Số bộ vi xử lý
	- Số lõi trên từng bộ vi xử lý

<img src="image/31.png">

- Thiết lập kích thước bộ (RAM)

	- Kích thước tối đa cho phép là 6320MB. 
	- Kích thước khuyến nghị là 1024MB. 
	- Kích thước tối thiểu là 512MB.

<img src="image/32.png">

- Kiểu kết nối mạng

	- Kiểu Bridge: Máy ảo sử dụng chung card vật ký với máy thật. Chung dải mạng với máy thậy và có thể ra ngoại internet
	- Nat: Máy ảo tạo 1 card mạng ra ngoài máy thật. Có teher ra ngoài internet
	- Hostonly:  Máy ảo tạo 1 card mạng ngoài máy thật và không thể ra ngoài internet 
	- Không sử dụng để kết nối mạng

Kiểu kết nối này có thể thay đổi được sau.

<img src="image/33.png">

<img src="image/34.png">

<img src="image/35.png">

- Lựa chọn ổ đĩa
	- Create a new vitual disk: Tạp 1 đĩa ảo mới
	- Use an existing virtual disk : Sử dụng 1 ổ đĩa hiện có. Chọn tùy chọn này để sử dụng lại đĩa được cấu hình trước đó
	- Use a physical disk ( for advanced users) Sử dụng ổ đĩa vật lý.

<img src="image/36.png">

- Thiết lập kích thước ổ đĩa
	- Kích thước khuyến nghị là 20GB
	- Allocate all disk space now: Phân bổ tất cả dung lượng đĩa ngay bây giờ
	- Store vitual disk as a single file: Lưu ổ đĩa cứng vào 1 file đơn
	- Split virtual disk into mutiple files: Chia ổ cứng thành nhiều file

<img src="image/37.png">

- Lưu file .vmdk (file đĩa ảo) Vào cùng thư mục máy ảo đã tạo ở bước trên 

<img src="image/38.png">

- Xem lại tất cả các cấu hình, thiết lập máy ảo rồi nhấn **Finish** để tiến hành cài đặt

<img src="image/40.png">

- Chọn Settings

<img src="image/41.png">

- Chọn file iso để cài đặt 

<img src="image/42.png">

- Lựa chọn ngôn ngữ trong quá trình cài đặt 

<img src="image/43.png">

- Chọn **Install Unbuntu Server** để tiến hành cài đặt

<img src="image/44.png">

- Lựa chọn ngôn ngữ sử dụng trong hệ điều hành Ubuntu. Chon **English** rồi nhấn **Enter**

<img src="image/45.png">

- Lựa chọn khu vực cài đặt 

<img src="image/46.png">

- Cấu hình bàn phím nếu cần. Ở đây mình chọn **No** không cấu hình gì thêm cho bàn phím. 

<img src="image/47.png">

- Cách bố trí bàn phím mỗi quốc gia là khác nhau, một quốc gia có thể có nhiều layout. Chọn Quốc gia xuất xứ cho bàn phím.

<img src="image/48.png">

- Chọn chuẩn cú pháp gõ bàn phím cho keyboard. Chọn English(US) 

<img src="image/49.png">

- Cấu hình tên máy 
<img src="image/50.png">

- Khai báo tên thật của người dùng này. Thông tin này sẽ được sử dụng cho các email được gửi bởi người dùng này cũng như bất kỳ chương trình nào hiển thị hoặc sử dụng tên thật của người dùng. 

<img src="image/51.png">

- Khai báo tên tài khoản. Tên phải bắt đầu bằng chữ cái in thường.

<img src="image/52.png">

- Thiết lập mật khẩu

<img src="image/53.png">

- Nhập lại mật khẩu

<img src="image/54.png">

- Do mật khẩu mình đặt bao mật chưa cao nên họ hỏi lại có chắc chắn sử dụng pass yếu hay đổi pass mới. Chọn **No** nếu bạn muốn đặt lại mật khẩu. Chọn **Yes** nếu chấp nhận dùng mật khẩu yếu

<img src="image/55.png">

- Bạn có muốn mã hóa thư mục Home để bảo mật hay không. Đây mình chọn **NO**

<img src="image/56.png">

- Time Zone hiện tại của bạn là Asia/phnom_Penh. Nếu chưa chính xác thì bạn lựa chọn lại. Ở đây mình chọn **yes**

<img src="image/57.png">

- Lựa chọn hình thức cấu hình chia các partition ổ cứng. ( Partition: các phân vùng ổ cứng)
	+ **Guided-use entire disk**: Sử dụng cho ổ cứng chưa từng được phân vùng, máy tính sẽ tự động format và định dạng cho từng vùng đã chia.
	+ **Guided-use entire disk and set up LVM** Tự động phân vùng bằng LVM, là một phương pháp cho phép ấn định không gian đĩa cứng thành những logical volume, khiến cho việc thay đổi kích thước các ổ đĩa dễ dàng hơn mà không phải sửa lại table của OS. Trong trường hợp bạn đã sử dụng hết phần bộ nhớ còn trống của partition và muốn mở rộng dung lượng thì LVM là một sự lựa chọn tốt.
	+ **Guided-use entire disk and set up encrypted LVM** Giống với lựa chọn 2 nhưng sẽ cài đặt mã hóa ổ cứng để tăng tính bảo mật.
	+ **Manual**: Phân vùng thủ công

Trình cài đặt sẽ hướng dẫn bạn phân vùng ổ đĩa, hoặc bạn có thể tự phân vùng. Với phân vùng được hướng dẫn thì bạn có thể xem lại và tùy chỉnh kết quả.
Nếu bạn không rành về phần này thì chọn  **Guided-use entire disk**

<img src="image/58.png">

- Lựa chọn ổ cứng cài đặt

<img src="image/59.png">

- Ghi nhứng thay đổi vào ổ đĩa và cấu hình LVM

<img src="image/60.png">

<img src="image/61.png">

<img src="image/62.png">

<img src="image/63.png">

- Cấu hình HTTP nếu thấy cần thiết. Đây mình bỏ trống và chọn **Continue**

<img src="image/64.png">

- Quản lý những nâng cấp hệ thống	
	- **No automatic updates:** Ko tự động cập nhật
	- **Install security updates automatically:** Cài đặt cập nhật bảo mật tự động
	- **Manage system with Landscape:** Quản lý hệ thống với Landscape

<img src="image/65.png">
- Lựa chọn một số phần mềm cài đặt cùng

<img src="image/66.png">

- Cài đặt GRUB boot loader lên ổ cứng để lựa chọn cấu hình ổ cứng. 

<img src="image/67.png">

- Sau khi chọn yes  ở trên, quá trình cài đặt OS bắt đầu và kết thúc khi xuất hiện bản thông báo hoàn tất quá trình. Chọn continue và máy sẽ tự restart.

<img src="image/68.png">
