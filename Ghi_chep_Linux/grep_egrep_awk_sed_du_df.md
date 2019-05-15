## du, df, grep, awk, sed

### 1. Command du

Command du kiểm tra chi tiết về dung lượng của từng thư mục hay tệp tin trong Linux. 

Option : 
- **-h**: Kích thước thư mục MB và GB
- **-a**: all file và thư mục
- **-s**: file hoặc thư mục cụ thể. 

### 2. Command df 
df- disk filesystem. Lệnh này kiểm tra phàn vùng, ổ đĩa của hệ thống tệp tin linux. 
```
[chint@localhost ~]$ df
Filesystem              1K-blocks    Used Available Use% Mounted on
/dev/mapper/centos-root  17811456 1882928  15928528  11% /
devtmpfs                   485996       0    485996   0% /dev
tmpfs                      497944       0    497944   0% /dev/shm
tmpfs                      497944    7788    490156   2% /run
tmpfs                      497944       0    497944   0% /sys/fs/cgroup
/dev/sda1                 1038336  166628    871708  17% /boot
tmpfs                       99592       0     99592   0% /run/user/1000
```
Phần trăm (%) dung lượng đã được sử dụng.

`df -h` : Dung lượng ổ đĩa hiện dưới dạng MB và GB

### 3. lsblk (list block devices)

Hiển thị các devices 

### 4. Grep

Lệnh `grep` để tìm chuỗi trong 1 file hoặc nhiều file

Command `grep -[option] chuỗi file`

- Option : 
	- **-i**: Lệnh grep phân biệt chữ hoa, chữ thường. option -i để laoij bỏ phân biệt này. 
	- **-w**: Tìm kiếm chính xác
	- **-v**: Tìm ngược. Tức là tìm dòng ko chứa chuỗi
	- **-l**: Hiển thị tên file
	- **-n**: Hiển số dòng của kết quả.
	- **-c**: Hiển thị số kết quả

- Ký tự Meta của grep
	- **+** - Tương đương với một hoặc nhiều lần xuất hiện của nhân vật trước đó.
	- **?**- Điều này biểu thị gần 1 lần lặp lại của nhân vật trước đó. Giống như: a?Sẽ khớp với 'a' hoặc 'aa' .
	- **(** - Bắt đầu biểu thức xen kẽ.
	- **)**- Kết thúc biểu thức xen kẽ.
	- **|**- Ghép một trong hai biểu thức cách nhau bởi '|'. Giống như: “(a|b)cde”sẽ khớp với 'abcde' hoặc 'bbcde' .
	- **{**- Ký tự meta này biểu thị bắt đầu của bộ xác định phạm vi. Giống như: “a{2}”khớp với aa canh trong tập tin tức là 2 lần.
	- **}** - Ký tự meta này biểu thị kết thúc của bộ xác định phạm vi.

- Lệnh grep: các ký tự meta bị mất ý nghĩa của chúng và bị coi như các ký tự bình thường. Cần phải đặt chúng trước ký tự thoat `\` để grep coi nó như các ký tự đặc biệt.

### 5. Egrep 

- Lệnh `egrep` là `grep` mở rộng. Một phiên bản khác của grep giúp quá trình tìm kiếm nhanh hơn khi tìm kiếm một biểu thức vì nó xử lý meta do đó không cần phải sử dụng lệnh `\`.

### 6. awk 

Awk là một ngôn ngữ lập trình hỗ trợ thao tác dễ dàng đối với kiểu dữ liệu có cấu trúc và tạo ra những kết quả được định dạng. Viết tắt tên của 3 tác giả: Aho, Weinberger và Kernighan.

Awk thường được sử dụng cho việc tìm kiếm và xử lý text

- Một số đặc điểm nổi bật của Awk:
	+ Nó xem 1 file text giống như bảng dữ liệu, bao gồm các bản ghi và các trường
	+ Tương tự những ngôn ngữ lập trình phổ biến, Awk cũng có những khái niệm như biến, điều kiện, vòng lặp
	+ Awk có những toán tử số học và toán tử thao tác chuỗi
	+ Awk nhận đầu vào là 1 file hoặc 1 input có dạng chuẩn, rồi tạo ra output theo dạng chuẩn đó. Awk chỉ làm việc với filetext.

Cú pháp: 
`awk '/search pattern 1/ {Actions} /search pattern 2/ {Actions}' filename`
Giải thích:
     - search pattern là một biểu thức chính quy
     - Actions là những câu lệnh sẽ được thực hiện
     - file: file đầu vào Awk sẽ chấp nhận một vài kiểu pattern và action.

- Cách thức hoạt động
	- Chương trình được viết với Awk đọc file đầu vào theo từng dòng một
	- Đối với mỗi dòng, nó sẽ so khớp dòng ấy lần lượt với các pattern, nếu khớp thì sẽ thực hiện action tương ứng
	- Nếu không có pattern nào được so khớp thì sẽ không có action nào được thực hiện
	- Trong cú pháp cơ bản khi làm việc với Awk, hoặc search pattern có thể vắng mặt, hoặc action có thể vắng mặt, nhưng không được khuyết cả 2
	- Nếu không có search pattern, Awk sẽ thực hiện action đã cho đối với mỗi dòng của dữ liệu đầu vào
	- Nếu action vắng mặt, Awk sẽ mặc định in ra tất cả những dòng khớp với pattern đã cho
	- Chương trình có cặp ngoặc nhọn không chứa action nào sẽ không thực hiện gì cả, kể cả thao tác mặc định (in ra tất cả các dòng)
	- Mỗi câu lệnh trong phần action được phân tách nhau bởi dấu chấm phẩy.
Theo mặc định, chương trình được viết với Awk sẽ in ra từng dòng của file đầu vào. 

Ví dụ : 
```
[chint@localhost dir1]$ cat file1
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
3 Ngoc Linh 7.8
4 Van Hoa 5.3
```

- Trong vies dụ này, không có sự xuất hiện của phần pattern, do đó lệnh print được áp dụng cho toàn bộ các dòng.
```
[chint@localhost dir1]$ cat file1
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
3 Ngoc Linh 7.8
4 Van Hoa 5.3
```

- In ra những dòng có chứa xâu mẫu

```
[chint@localhost dir1]$ awk '/Hoang/' file1
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
```

- Theo mặc định awk chia bản ghi này ra thành từng trường ngăn cách nhau bởi các khoảng trắng và lưu trong các biến có dạng $n. Nếu một dòng có 4 từ, các từ ấy sẽ được lưu trong các biến $1, $2, $3 và $4. $0 đại diện cho toàn bộ dòng. NF là biến dựng sẵn lưu giữ giá trị tổng số trường của một bản ghi.

```
[chint@localhost dir1]$ awk '{print $3, $4}' file1
Anh 6.7
Hanh 8.9
Linh 7.8
Hoa 5.3
```

```
[chint@localhost dir1]$ awk '{print $3, $NF}' file1
Anh 6.7
Hanh 8.9
Linh 7.8
Hoa 5.3
```

- **Phép so sánh**

```
[chint@localhost dir1]$ awk '$4>7.5' file1
2 Hoang Hanh 8.9
3 Ngoc Linh 7.8
```

- **Cú pháp điều kiện**

Giả sử chúng ta muốn in ra danh sách những sinh viên họ Hoàng
```
[chint@localhost dir1]$ awk '$2~/Hoang/' file1
1 Hoang Anh 6.7
2 Hoang Hanh 8.9
```
Toán tử ~ (thuật ngữ tiếng Anh tương ứng là tilde) được dùng để so sánh giá trị của một trường với một biểu thức chính quy. Nếu kết quả là khớp, dòng dữ liệu đó sẽ được in ra màn hình.

- **Tính toán số học**

Chương trình dưới đây thực hiện đếm số sinh viên họ Hoang nếu có thì giá trị của biến count được tăng lên 1 đơn vị. Biến này được khởi tạo giá trị ban đầu bằng 0 với từ khóa BEGIN.

```
[chint@localhost dir1]$ awk 'BEGIN {conut=0}
> $2~/Hoang/ {count++}
> END {print "Ketqua =", count}' file1
Ketqua =2
```
**Tài liệu tham khảo:** https://viblo.asia/p/tim-hieu-awk-co-ban-gGJ59229KX2


### 7. Sed

Sed, như cái tên của nó Stream EDitor, dùng để thao tác trực tiếp với văn bản như thay thế, xóa dòng, in ra một số dòng v.v.. 

#### 7.1. Cú pháp chính

Sed dùng để thay thế sự xuất hiện của 1 chuỗi bằng chuỗi khác trong 1 văn bản. 

**Cú pháp:** `sed 's/pattern/replace_string/' filename`

Hoặc: `cat filename | sed 's/pattern/replace_string/'`

Trong đó: 
	- pattern: có thể là 1 chuỗi ký tự hoặc 1 biểu thức chính quy
	- replace_string: Là 1 chuỗi thay thế

Nếu sử dụng trình soạn thảo vim: `%s/pattern/replace_string/` thì kết quả cũng tương tự. 

#### 7.2. Lưu các thay đổi vào tệp tin

Cú pháp trên chỉ in ra văn bản thay thế. Để lưu thay đổi, sử dụng tùy chọn -i. Phần lớn người dùng thực hiện chuyển hướng để lưu tập tin sau khi thay đổi như sau: 

`sed 's/text/replace/' filename > newfile`

Nếu không chuyển hướng file thực hiện lệnh sau 

`sed -i 's/text/replace/' filename`

#### 7.3. Ký tự dấu phân cách

Các ví dụ trên sử dụng `/` làm lý tự dấu phân cách, ngoài ra có thể dùng `|` và `:`

Khi dấu phân cách xuất hiện trong mẫu ta phải thoát nó bằng sử dụng tiền tố `\`.

#### 7.4. Xóa các dòng trống

Tham chiếu các dòng trống bằng biểu thức chính quy `^$`

`sed '/^$/d' filename`

***/pattern/d***: Sẽ xóa các dòng trùng khớp với pattern

**Tài liệu tham khảo**:
https://www.justpassion.net/tech/programming/bash-shell/lenh-sed-trong-linux.html