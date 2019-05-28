## System local, keybroad 

### 1. Set system local 
Cài đặt cấu hình hệ thống được lưu trong `etc/locale.conf` (CentOs/RedHat), `etc/default/locate` (Debian), Hoạc sử dụng lệnh `locatectl`

#### 1.1. Display the Current Status 

Lệnh localect có thể sử dụng để truy vấn và thay đổi vị trí hệ thống, bố cục bàn phím. Để show cài đặt hiện tại, sử dụng status option.

```
[user@centos7 etc]$ localectl status
   System Locale: LANG=en_US.UTF-8
       VC Keymap: us
      X11 Layout: us
```

Đầu ra chứa vị trí cài đặt hiện tai, bố cục bàn phím được cấu hình và hệ thống cửa sổ X11.

#### 1.2. Listing Available Locales

```
[user@centos7 etc]$ localectl list-locales| grep en
en_AG
en_AG.utf8
en_AU
en_AU.iso88591
en_AU.utf8
.....
```

#### 1.3.Setting the Locale

Command: 

`localectl set-locale LANG=locale`

Eg: localectl set-locale LANG=en_GB.utf8

### 2. Changing the Keyboard Layout
Cài đặt bố cục bàn phím cho phép người dùng khiểm soát bố cục được sử dụng trên bảng điều khiển hoặc giao diện người dùng đồ họa.

#### 2.1. Displaying the current Settings

Command: `localectl status` 

#### 2.2. Listing Available Keymaps

Comamnd: `localectl list-keymaps`

Có thể sử dụng grep để tìm kiếm 

Vi dụ: localectl list-keymaps | grep cz

#### 2.3. Setting the Keymap

Để đặt bố cục bàn phím mặc định cho hệ thống:

Command: `localectll set-keymap map`

Thay thế map được lấy từ keymap đầu ra. Option **–no-convert** được áp dụng. Cài đặt đã chọn được áp dụng cho ánh xạ bàn phím mặc định của hệ thống cửa sổ X11, sau khi chuyển nó thành keyboard X11 phù hợp nhất. 

Command: **localectl set-x11-keymap map**

Nếu bạn muốn bố cục X11 của mình khác với bố cục bảng điều khiển, sử dụng option **--no-convert**

Command: **localectl --no-convert set-x11-keymap map**

Eg: **localectl --no-convert set-x11-keymap de**

