SUID SGID Sticky Bit Chỉ số umask 

### Sticky Bit(t)
Làm tăng  nó làm tăng tính bảo mật của một tập tin / thư mục được chia sẻ với những người dùng khác. Khi Sticky Bit được bật, chỉ người dùng (chủ sở hữu) của tệp đó có thể xóa hoặc đổi tên tệp ngay cả khi người dùng khác có quyền (rwx) đầy đủ trên tệp đó. Chủ yếu là bit dính được sử dụng trên các thư mục mà nhiều người dùng có quyền truy cập như /tmp. 

### SUID (Set User ID) Bits
Khi bit SUID được bật trên tập tệp, bất cứ khi nào ai đó thực thi tệp, nó sẽ chạy với tư cách là người dùng là chủ sở hữu của tệp đó. Nó có nghĩa là tệp được đảm bảo để chạy với tư cách là chủ sở hữu, ngay cả khi được thực thi bởi bất kỳ ai. Điều này rất hữu ích khi bạn muốn trao quyền thực thi của tập lệnh đặc quyền gốc cho một số người dùng khác. Đây là lý do người dùng có thể tự thay đổi mật khẩu của mình.

Chủ yếu chúng tôi kích hoạt bit SUID trên các tệp đặc biệt trên các tập lệnh thực thi.

### SGID Bit (Set Group ID bit)

Khi bit SGID được bật trên một thư mục, bất kỳ tệp/thư mục nào được tạo bởi nó bởi bất kỳ người dùng nào cũng có quyền nhóm giống như của thư mục mẹ.

**Thay đổi quyền nâng cao của file**

Chmod cho SUID, SGID, Sticky Bit
|Permission|Chế độ tượng trưng|Chế độ số|
|:---:|:---:|:---:|
|Sticky Bit|chmod +t file_name|chmod 1XXX file_name|
|SGID|chmod g +s file_name|chmod 2XXX file_name|
|SUID|chmod u +s file_name|chmod 1XXX file_name|

### 4. Chỉ số umask 

Quyền truy cập chính thức của 1 file dựa trên 2 giá trị là quyền truy cập cơ sở( base permission) và mặt mạ (mask)
- Base Permission: Là giá trị được thiết lập từ trước, không thể thay đổi được. Khi tạo 1 file hệ thống đã gán cho nó quyền đó.]
	+ File thông thường: 666 (rw-rw-rw-)
	+ File đặc biệt ( thư mục): 777 (rwxrwxrwx)
- Mask: là giá trị đựợc thiết lập bởi người dùng bằng lệnh umask
Giá trị Mask sẽ “che đi” một số bit trong Base Permission để tạo ra quyền truy cập chính thức cho file
	+ Mặc định mask user =002
	+ Mask root =022

- Xem umask 
`umask` =>enter 
- Thay đỏi umask 
VD : umask 027

Quyền truy cập chính thức được tính bằng cách lấy“giá trị nhị phân của Base permission ”AND“ dạng biểu diễn bù 1 của mask”

Ví dụ:  Base Permission của file bất kỳ luôn là 666 (tức 110110110 khi chuyển sang dạng nhị phân), nên nếu giá trị mask là 022 (có dạng nhị phân là 000010010 => dạng bù 1 của nó thì chuyển 1->0, 0->1 nên ta được 111101101) thì quyền truy nhập chính thức của file sẽ là:

110 110 110 AND 111 101 101 = 110 100 100 = 644 (rw-r–r–)

Cũng có thể tính quyền truy cập chính thức đơn giản hơn bằng cách lấy 666 – 022 = 644

**Tài liệu tham khảo:** http://linuxsuperuser07.blogspot.com/2012/08/suid-sgid-and-sticky-bit-in-rhel6.html