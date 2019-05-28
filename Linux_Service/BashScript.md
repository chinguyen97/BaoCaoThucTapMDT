### Bash Script 

Trong Linux làm việc với các câu lệnh là rất quan trọng và cần thiết. Tuy nhiên nó gặp phải 1 số điều sau: 
- Chỉ làm được 1 công việc 1 lúc, không thể làm 2 công việc trở lên.
- Các chương trình phải hoạt động theo một thứ tự nhất định để thực hiện một công việc nào đó và nếu thay đổi thứ tự này sẽ dẫn đến việc xử lý công việc khác.
- Có một số công việc phải làm với tất suất rất lớn và đôi khi là lặp đi lại trong thời gian ngắn.

**Bash Scrip** ra đời khắc phục những vấn đề trên. Các Scrip viết ra có thể thực hiện công việc ngay lập tức thay vì gõ hàng loạt các câu lệnh.

#### 1. Khái niệm

Bash Script là một loại ngôn ngữ kịch bản thường đc viết bởi con người và được thực thi bởi ngôn ngữ máy. Bash script cũng có riêng một trình thông dịch đó là BASH (Bourne Again SHell)

Viết tất cả các câu lệnh cần thiết vào một file Bash (\*.sh) và thực thi nó. Cần cung cấp quyền thực thi cho file Bash. 


#### 2. Tìm hiểu file bash scrip

- Tạo file bash 

Một file Bash phải bắt đầu bằng dòng ký tự `#!(shebang)` 

```
#!/bin/bash
```
Dòng ký tự này sẽ thông báo cho HĐH biết file script này sẽ được thực thi bởi chương trình nào. 

Để biết chính xác trình thông dịch của Bash nằm ở đâu, bạn có thể dùng which bash:

```
[user@centos7 ~]$ which bash
/bin/bash
```
- Tên file .sh
Ví dụ: Tạo 1 file đơn giản

```
#!usr/bin/bash 
echo "Linux Learning"
echo "Hello Hello"
```
Đặt tên file: test.sh

Chạy file: `bash test.sh`

Hoặc: `./test.sh` trước đó cần thèm quyền +x cho file

`chmod +x test.sh`


### 3. Làm việc vơi biến

Biến là khái niệm dùng để chỉ các phần dữ liệu được lưu trữ tại một ô nhớ cụ thể trong bộ nhớ và có thể gọi trực tiếp qua tên.

Tên biến chứa các ký tự (a-z), các số (0-9), dấu gach dưới_

Tên biến không chứ các ký tự: !, \*, -, không bắt đầu bằng 1 số. 

- Định nghĩa một biến 

`variable_name=variable_value`
Ví dụ: a='30', NAME="CHI", Var=100.

- Truy cập các giá trị trong biến 

Sử dụng ký hiệu dollar ($) ngay trước tên biến. 
Ví dụ: 
```
#!/bin/bash
AGE=30
echo $30
```
- Biến chỉ đọc(read-only)

Một biến được đánh dấu read-only bằng cách thêm lệnh readonly, giá trị của nó không thể thay đổi được. 
Ví dụ:

```
#!usr/bin/bash 
NAME="CHINGUYEN"
readonly NAME
NAME="NGUYENCHI"
echo $NAME
```

```
[user@centos7 ~]$ bash test.sh
test.sh: line 4: NAME: readonly variable
CHINGUYEN
```

- Xóa 1 biến: Sử dụng lệnh ***unset***

```
#!usr/bin/bash 
NAME="CHINGUYEN"
unset NAME
echo $NAME
```

```
[user@centos7 ~]$ bash test.sh

[user@centos7 ~]$ 
```

Có thể lưu đầu ra của một câu lệnh khác vào một biến bằng cách sử dụng một trong 2 cách sau:
	- Dùng dấu backtick: **var_name=`command`**
	- Dùng dấu dollar: **var_name=$(command)**


- Các biến đặc biệt 
Ký tự $ đại diện cho số Process ID hoặc PID của shell hiện tại.

```
[user@centos7 ~]$ echo $$
7289
```
https://vietjack.com/unix/cac_bien_dac_biet_trong_unix_linux.jsp



### 4. Sử dụng mảng

Mảng cho phép lưu trữ nhiều giá trị tại cùng một thời điểm.

- Định nghĩa mảng: 
	+ Định nghĩa 1 mảng sử dụng 1 danh sách các giá trị trong 1 dòng như sau: `Day=(monday, tuesday,wednesday, thursday, friday, satuaday, sunday)`
	+ định nghĩa 1 mảng như 1 tập các cặp chỉ mục – giá trị như sau:

```
Day[0]="monday"
Day[1]="tuesday"
Day[2]="wednesday"
```
- In nội dung 1 giá trị trong mảng

`echo ${Day[2]}`

- In nội dung tất cả các gía trị trong mảng như 1 danh sách: `echo ${Day[*]}`

Hoặc: `echo ${Day[@]}`

- In chiều dài của mảng

`echo ${#Day[*]}`


### 5. Các toán tử Shell cơ bản

1. Toán tử logic
Khai báo 2 biến; a=10; b=20.
- Toán tử `+` cộng: `expr $a + $b`
Chú ý: Phải có khoảng trống giữa 2 toán tử: Ví dụ: 2 + 2 (Đúng), 2+2 (Sai)
- Toán tử `+` cộng: `expr $a + $b`
- Toán tử `-` trừ: `expr $a - $b`
- Toán tử `*` nhân: `expr $a * $b`
- Toán tử `/` chia: `expr $a / $b`
- Toán tử `%` lấy số dư: `expr $a % $b`
- Toán tử `=` phép gán: `a = $b` Gán gái trị của a cho b
- Toán tử `==` phép bằng: [ $a == $b ] Sẽ trả về kết quả False
- Toán tử `!=` phép không bằng: [ $a != $b ] Sẽ trả về kết quả True

2. Toán tử quan hệ 



### 6. Câu điều kiện

Bash hỗ trợ 3 dạng câu điều kiện

- Dạng 1: Chỉ gồm 1 điều kiện

```
if conditional; then
	statement_1
else 
	statement_1
fi
```
- Dạng 2: Gồm 2 điều kiện trở lên

```
if conditiona_1; then
	statement_1
elif conditional_2; then
	statement_2
else 
	statement_3
fi
```
- Dạng 3: Các câu lệnh lồng nhau: 

```
if conditiona_1; then
	if conditional_2; then
		statement_1
	else 
		statement_2
	fi
fi
```

Ví dụ: 
```
[user@centos7 ~]$ cat test.sh 
#!/bin/bash
a=`10`;
if $a > 5; then
	echo "Hello Hello"
else
exit
fi
```

https://viblo.asia/p/don-gian-hoa-tac-vu-trong-linux-voi-bash-script-phan-1-gGJ59gaGZX2
