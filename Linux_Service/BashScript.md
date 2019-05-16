### Bash Script 

Trong Linux làm việc với các câu lệnh là rất quan trọng và cần thiết. Tuy nhiên nó gặp phải 1 số điều sau: 
- Chỉ làm được 1 công việc 1 lúc, không thể almf 2 công việc trở lên.
- Các chương trình phải hoạt động theo một thứ tự nhất định để thực hiện một công việc nào đó và nếu thay đổi thứ tự này sẽ dẫn đến việc xử lý công việc khác.
- Có một số công việc phải làm với tất suất rất lớn và đôi khi là lặp đi lại trong thời gian ngắn.

**Bash Scrip** ra đời khắc phục những vấn đề trên. Các Scrip viết ra có thể thực hiện công việc ngay lập tức thay vì gõ hàng loạt các câu lệnh.

#### 1. Khái niệm

Bash Script là một loại ngôn ngữ kịch bản thường đc viết bởi con người và được thực thi bởi ngôn ngữ máy. Bash script cũng có riêng một trình thông dịch đó là BASH (Bourne Again SHell)

Viết tất cả các câu lệnh cần thiết vào một file Bash (\*.sh) và thực thi nó. Cần cung cấp quyền thực thi cho file Bash. 

#### 1. Các cú pháp cơ bản trong Bash Script

Các bước thực hiện: 
- Taoj file script 
```
#!/bin/bash
....
```
tên file .sh
Chạy file `bash tên file`

Cah
./filename

#### 2. Tìm hiểu file bash scrip

- Tạo file bash 
Một file Bash phải bắt đầu bằng dòng ký tự `#!(shebang)` 
`#!/bin/bash`
Dòng ký tự này sẽ thông báo cho HĐH biết file script này sẽ được thực thi bởi chương trình nào. 

Để biết chính xác trình thông dịch của Bash nằm ở đâu, bạn có thể dùng which bash:

```
[user@centos7 ~]$ which bash
/bin/bash
```

- Tên file .sh

- Variable trong bash 
Biến là khái niệm dùng để chỉ các phần dữ liệu được lưu trữ tại một ô nhớ cụ thể trong bộ nhớ và có thể gọi trực tiếp qua tên.
Cách sử dụng biến: 
- Để khai báo 1 biến, ta sử dụng ký hiệu equal (=) giữa tên biến và giá trị của biến. Ví dụ: a=`30`
- Truy cập tới 1  biến, sử dụng ký hiệu dollar ($) ngay trước tên biến. 
Vd: `$a`


Một số chương trình cần truyền tham số dòng lệnh vào để sử dụng, Bash cho phép sử dụng một số biến đặc biệt sau:

$0: Tên của file script.
$1 -> $9: Các tham số truyền vào
$#: Số lượng của tham số truyền vào
$\*: Danh sách các tham số được truyền vào
(các trường hợp $# và $\* sẽ không bao gồm $0)


Đặc biệt, có thể lưu đầu ra của một câu lệnh khác vào một biến bằng cách sử dụng một trong 2 cách sau:

Dùng dấu backtick
var_name=`command`
Dùng dấu dollar
var_name=$(command)

### Câu điều kiện

Bash hỗ trợ 3 dạng câu điều kiện
- 



https://viblo.asia/p/don-gian-hoa-tac-vu-trong-linux-voi-bash-script-phan-1-gGJ59gaGZX2












protocol, proxy