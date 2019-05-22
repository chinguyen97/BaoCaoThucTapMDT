## File /etc/hosts

### 1. Tìm hiểu file /etc/hosts

Mỗi địa chỉ website trên Internet đều được liên kết với một địa chỉ ip duy nhất qua hệ thống DNS (Domain Name System). Hệ thống DNS này giúp ánh xạ các địa chỉ ip vốn rất khó nhớ với tên miền có ý nghĩa giúp bạn dễ nhớ khi truy cập website.

File hosts là môt tập tin được sử dụng để xác định địa chỉ tên miền nào được liên kết với địa chỉ ip nào tương tự như DNS. Hệ thống sẽ kiểm tra file host trước khi tìm kiếm một trang web trên các máy chủ DNS được xác định trong cài đặt mạng

- Tùy vào từng hệ điều hành mà vị trí của file host cũng khác nhau.
	- Đối với máy tính Windows thì file host nằm ở: **C:\Windows\System32\drivers\etc\hosts**
	- Đối với hệ điều hành Linux thì vị trí của file host: **/etc/hosts**

Nội dung của file host là các dòng mà mỗi dòng có 2 trường phân cách bởi một hoặc nhiều dấu **tab**. Có cấu trúc: <địa chỉ IP> <tên miền>

Địa chỉ IP có thể là tĩnh hoặc động. File host như là một DNS server của máy tính. Khi bạn truy cập vào tên miền nào sẽ vào IP đó. Trong file hosts mặc định sẽ là: 127.0.0.1 localhost

Máy tính truy cập vào mạng sẽ có một địa chỉ ip riêng, ngoài ra còn có một địa chỉ ip khác là 127.0.0.1 chính là địa chỉ IP cục bộ của máy tính. Đây là địa chỉ đặc biệt được gọi là localhost. Khi ta truy cập tới thiết kế web trên, máy tính sẽ cố thực hiện kết nối tới chính bản thân nó. Vì thế, kết nối không thể tìm thấy server và ngăn chặn hiệu quả quá trình tải website về máy của bạn.

### 2. Công dụng của file host

- Chặn Website

Để ngăn chặn Website, bạn chỉ cần bổ sung thêm một dòng có cú pháp: 127.0.0.1 tên website ở cuối file hosts.

Ví dụ: Muốn chặn Facebook: `127.0.0.1	www.facebook.com`

Trình duyệt đọc file hosts sau đó sẽ gửi request (yêu cầu) đến địa chỉ ip 127.0.0.1. 127.0.0.1 là địa chỉ IP loopback sẽ luôn trỏ về hệ thống của riêng bạn. Vì trang web không được lưu trữ trên máy, nên trình duyệt sẽ cho biết trang web không thể được tìm thấy. Bây giờ, trang web đã bị chặn một cách hiệu quả.

- Chuyển hướng website

Người dùng có thể sử dụng file host để chuyển hướng từ website này sang website khác. Vì dụ: Sau khi bạn chuyển hướng từ twitter sang facebook.com, thì khi bạn nhập twitter vào thanh địa chỉ trình duyệt thì điểm đến sẽ là facebook.

Đầu tiên, bạn chỉ cần biết địa chỉ IP của trang facebook. Cách tìm địa chỉ bằng câu lện ping trong cừa sổ dòng lệnh. Bạn gõ ping facebook vào cửa sổ lệnh để xem địa chỉ IP của trang.

`157.240.15.35 https://twitter.com/`

Bây giờ, bạn chỉ cần thêm dòng sau vào file hosts: 199.59.150.39 twitter đế máy tính liên kết tên miền twitter với địa chỉ IP của facebook.

- Truy cập nhanh Website

Bạn cũng có thể sử dụng file host đến những thiết kế website chuyên nghiệp từ bất kỳ trình duyệt nào trên máy tính. Ví dụ: bạn là một tín đồ của facebook và bạn gán f cho facebook thì khi bạn gõ f trình duyệt tự động hiểu và hiển thị ra trang facebook cho bạn.

Để làm điều này, bạn chỉ cần bổ sung dòng: 199.59.150.39 f tới file hosts và lưu lại.

Nhiều khi bạn cảm thấy bực bội khi truy cập vào một website nào đó mà phải chờ quá lâu mới tải hết trang. Chắc hẳn là website đó chưa thật sự được tối ưu tốt. Bởi lẽ, các đơn vị cung cấp dịch vụ SEO chuyên nghiệp, tốc độ truy cập website là một yếu tố rất được chú trọng.
Ấn định các tên miền cục bộ


https://gocinfo.com/chinh-sua-file-hosts-tren-windows-linux.html
https://quantrimang.com/sua-doi-quan-ly-file-hosts-tren-linux-162444
https://www.thuysys.com/co-ban/huong-dan-thay-doi-file-hosts-va-hostname-tren-linux.html
