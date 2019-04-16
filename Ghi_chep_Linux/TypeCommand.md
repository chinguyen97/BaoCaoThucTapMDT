### Type Command

Command: Lệnh là 1 chỉ dẫn được đưa ra bởi người dùng để 1 máy tính có thể thực hiện nó.

### 1. Phân loại 
Commmand thường được chia làm 4 loại: 
- **Type1- shell builtin**. Lệnh được xây dựng bởi chính shell. Bash cung cấp 1 số câu lệnh bên trong gọi là shell builtin. 
 VD: cd, echo, enable, help, kill, type, return,[...
- **Type2: Loại chương trình thực thi** như tất cả các tệp mà chúng ta đã thấy trong / usr / bin. Các chương trình có thể được biên dịch các nhị phân như các chương trình được viết bằng C và C ++ hoặc các chương trình được viết bằng các ngôn ngữ script như shell, Perl, Python, Ruby, v.v
VD: cp is /bin/cp, rm, mv, 
- **Type3: aliased to `ls --color=auto`**. Các tệp và thư mục sẽ có màu khác nhau nhờ tùy chọn --color. 
Vd: ll, l, ls, la, grep, egrep, fgrep,elert.
- **Type4: shell keywork**
VD: if, else, then, do, in, funtion, time,[[...

### 2. Các câu lệnh

- Kiểm tra type command:
Cú pháp: `type command`

Ví dụ: 
```
$ type type
$ type is a shell builtin
$type ls
$ls is aliased to `ls --color=autor`
$type cp
$cp is /bin/cp
```

- Liệt kê các Shell builtins: 
  `compgen -b`
- Liệt kê Shell Keywords:
  `compgen -k`
- Liệt kê các aliased:
  `compgen -a`


 Tài liệu tham khảo: http://linuxcommand.org/lc3_lts0060.php
  
