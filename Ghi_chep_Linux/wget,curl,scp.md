
## Command: wget, curl, scp

Môi trường: CentOS7

### 1. gwet

1. Giới thiệu

Wget là 1 tiện ích miễn phí download các file từ internet. Hỗ trợ cacs giao thức HTTP, HTTPs, FTP, SFTP, cũng như truy xuất qua HTTP proxy 

wget is non-interactive (Không tương tác) có nghĩa là nó có thể hoạt động ở chế độ nền, trong khi người dùng chưa đăng nhập, cho phép bạn bắt đầu truy xuất và ngắt kết nối khỏi hệ thống, cho phép wget hoàn thành công việc.

2. Cài đặt wget

`sudo yum install wget`

3. Command

- Cú pháp chung: `wget URL`

VD: `wget https://9mobi.vn/cf/images/2015/03/nkk/anh-dep-1.jpg`

- Có thể tải cùng lúc nhiều file

`wget URL1 URL2 URL3`

- Ngoài ra có thể đặt tất cả các fiel cùng tải trong 1 file:

VD: 
```
cat file 1
URL1
URL2
URL3
```

Sử dụng tùy chọn -i đế lấy tất cả các file chứa trong file1. 

`wget -i file1`

- Lưu tập tin với tên khác

Thông thường tệp tin tải về có tên giống tên của tập tin trong đường dẫn URL, thông tin về quá trình tải được hiện ra trên màn hình. 

Tuy nhiên có thể tải về và lưu với tên khác bằng cách sử dụng tùy chọn -O. Nếu tên đó đã tồn tại thì nó sẽ ghi đè lên tập tin đang có. 

Thay vì hiển thị thông tin quá trình cài đặt ta có thể lưu nó trong 1 file riêng bằng cách sử dụng tùy chọn -o. 

- Tự động tải lại khi tệp bị lỗi. 

Trong quá trình tải do gặp sự cố => Tải thất bại. wget sẽ tự động tải lại. -t (tries)

`wget -t n URL `

trong đó: n là số lần tải lại. 
Nếu ko đặt n thì wget sẽ tải lại cho đến khi tải thành công thì thôi. 

Nếu chúng ta không muốn chỉ định số lần tải lại mà muốn wget lặp lại việc tải cho đến khi thành công mới dừng lại, trong trường hợp này ta thực hiện như sau:

`wget -t o URL`
 
- Lưu file tải về đến 1 thư mục chỉ định

Sử dụng tùy chọn -P

`wget -P Desktop/Tailieu URL`

File tải về sẽ xuất hiện trong thưc mục: Desktop/Tailieu

- Giới hạn tốc độ và định mức tải

Khi băng thông internet giới hạn và nhiều ứng dụng cùng chia sẻ kết nối  này, và nếu cần tải 1 tập tin lớn, nó sẽ chiếm hết băng thông của các ứng dụng khác, làm cho các ứng dụng này không hoạt động được.

Để giới hạn tốc độ tải trong wget, sử dụng tham số --limit-rate 

`wget --limit-rate 20k http://example.com/file.jpg`

 Trong đó: 
 - k: Kilobyte (KB)
 - m: Megabyte (MB)

Chúng ta cũng có thể chỉ rõ định mức tối đa cho việc tải. Việc tải sẽ dừng lại khi đạt đến định mức.

Để định hạn mức cho việc tải, sử dụng tham số –-quota hoặc -Q như sau:

`wget -Q 100m http://example.com/file1 http://example.com/file2`

- Bắt đầu lại và tải tải
nếu việc tải bị gián đoạn trước khi nó hoàn tất, có thể bắng đầu lại 

`wget -c URL`

- Sao chép toàn bộ trang web 

wget có thể tải toàn bộ URL trong 1 trang web. Sử dụng tùy chon --mirror

`wget --mirror --convert-links example.com`

Trong đó: 
	- mirror: Tải theo dạng đệ quy
	- convert -links: Tất cả các links sẽ đc chuyển thành link offline

Hoặc sử dụng lệnh sau:

`wget -r -N -k -l DEPTH URL`

-l  => chỉ ra độ sâu của các trang web dưới dạng các cấp. Điều này nghĩa là wget sẽ chỉ đi qua số lượng cấp mà chúng ta chỉ định.
DEPTH => độ sâu của trang web.
-r (recursive) => đệ quy, được dùng chung với -l.
-N được dùng để kích hoạt khóa thời gian cho tập tin.
URL là đường dẫn cơ sở cho 1 website nơi việc tải cần được khởi tạo
-k hoặc –convert-links => chỉ thị cho wget chuyển đổi các liên kết đến các trang khác trong trang được tải đến bản sao cục bộ của các trang đó.

Ngoài ra để tải 1 trang web về máy, chúng ta có thể sử dụng lệnh lynx như sau:

`lynx -dump URL > file.txt`

- Chứng thực HTTP hoặc FTP

Một số trang web yêu cầu chứng thực: Sử dụng các đối số: -user và -password

`wget --user username --password pass URL`

Việc nhập mật khẩu dưới dạng văn bản thô trong nội dung câu lệnh như trên sẽ không bảo mật và an toàn. Trong trường hợp này, chúng ta nên thay thế **–password** bằng **–ask-password** như sau:

`wget --user username --ask-password URL`

Password for user 'username': <Mật khẩu sẽ không hiển thị ra màn hình>

- Tải file trong Background

Với file cực lớn, có thể sử dụng function -b. Nó sẽ chạy ẩn dưới nền. 

`wget -b URL`

1 file wget-log sẽ xuất hiện trong thư mục hiện hành, bnaj có thể kiểm tra tiến trình và tình trạng. 

`tail -f wget-log`

- tải file theo số

Nếu có hình hoặc file đánh số theo 1 danh sách, có thể tải theo cấu trúc: 
`wget http://example.com/images/{1..50}.jpg`

***tài liệu tham khảo***

[1] https://www.justpassion.net/tech/programming/bash-shell/lenh-wget-trong-linux.html

[2] https://www.hostinger.vn/huong-dan/lam-nao-de-su-dung-wget-command/


###2. Curl (Client for URLs)

1. **Giới thiệu**

curl là cong cụ chuyển dữ liệu từ server hoặc đến server. Hỗ trợ nhiều giao thức(DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET and TFTP). Làm việc với giao diện dòng lệnh. 

2. **Cài đặt curl**

`yum insatll curl`

3. **Câu lệnh cơ bản**

- ***Cú pháp**: `curl <option> url`

Ví dụ: `curl https://www.google.com`

Trong trường hộ này dữ liệu html sẽ hiển thị trên terminal. Muốn lưu nó vào 1 file 

`curl https://www.google.com >google.html`

Hoặc dùng tùy chọn -o ` curl -o google.com https:://www.google.com`

Tùy chọn -O lưu 1 file cùng tên mà nó sử dụng trên máy chủ. 

VD: `curl -O  https://www.google.com`

- ***Tiếp tục tải xuống quá trình bị dừng***. 

Giả sử bạn tải xuống với lệnh 
`curl -O URL`

Sau đó nhấn Ctrl +C để dừng lại. 
Để tiếp tục quá trình tải: `curl -C - -O URL`

- ***Xác thực HTTP:*** 

`curl -u username:password -O URL`

- ***Giới hạn băng thông:***

`curl URL --limit-rate 20k`


***Tài liệu tahm khảo***

https://www.justpassion.net/tech/programming/bash-shell/lenh-curl-trong-linux-2.html


#### So sánh wget và curl 

- Giống
	- Cả 2 đều download nd từ HTTP, HTTPs, FTP.
	- Đều gửi đc HTTP POST request 
	- Hỗ trợ HTTP cookies

- Khác. 
	- Wget: Download nhanh, Download đệ quy
	- curl: Hỗ trợ gzp và tự động giả nén, Hỗ trợ nhiều giao thức hơn


### 3. SCP

1. Giới thiệu

- SCP (Secure Copy – Sao chép an toàn) là một ứng dụng sử dụng SSH để mã hóa toàn bộ quá trình chuyển tập tin.
- SCP là lệnh dùng để di chuyển file dữ liệu giữa các máy tính chạy hệ điều hành Linux từ xa chỉ cần biết địa chỉ ip
- SCP dùng ssh để di chuyển dữ liệu, có chế độ bảo mật giống như ssh.

2. Cài dặt 

Đa phần SCP có sẵn trong các bản phối của linux. Nếu chưa có, cài đặt như sau:

`yum install scp`

Cài đặt gói ssh trên các máy: 

`yum install openssh-server`

3. Sử dụng

- Copy file từ local đến Remote Server 

`scp /path/to/local/file.txt user@IP:/remote/path/`

Option :
- v: Hiển thị quá trình sao chép(in ra các thông tin gỡ lỗi trên màn hình)
- p: ƯỚc tính thời gian và tốc độ truyền, giữ nguyên thuộc tính file gốc
- C: Truyền tệp của nhanh hơn. Thông số -C sẽ nén tệp khi đang di chuyển. Quá trình nén chỉ xảy ra trong mạng khi truyền tệp. Khi tệp được gửi đến máy chủ đích, tệp sẽ trở lại kích thước ban đầu như trước khi quá trình nén xảy ra.
- c: mặc định SCP sử dụng AES-128 để mã hóa các tệp. Nếu ta muốn thay đổi cách mã hóa, ta có thể sử dụng tham số -c: 
VD: `scp -c 3des file1 user@192.168.1.10:/home/user`
- l: Giới hạn băng thông sử dụng. Nó sẽ hữu ích nếu 1 tệp dung lượng lớn, nhưng không muốn băng thông bị cạn kiệt bởi quá trình scp. 
VD: `scp -l 400 file1 user@192.168.1.10:/home/user`

Giá trị 400 cso nghĩa là giới hạn băng thông chi 50KB/ giây. Băng thông đc xác định bằng kbps. Trong scp tính bằng (KB/s). 50x8=400
- P: THông thường scp sử dụng cổng 22. Nhưng vì lý do bảo mật ta có thể thay thành cổng khác.
VD: `scp -P 2249 file1 user@192.168.1.10:/home/user`
- r: Sao chép đệ quy thư mục: Đôi khi chúng ta cần sao chép thư mục và tất cả các tệp tin bên trong nó
- q: (quiet mode) output sẽ bị chặn, tiến độ thực hiện sẽ k hiển thị ra. 

***Tài liệu tham khảo***
https://viblo.asia/p/10-scp-commands-to-transfer-filesfolders-in-linux-oOVlY40oZ8W
