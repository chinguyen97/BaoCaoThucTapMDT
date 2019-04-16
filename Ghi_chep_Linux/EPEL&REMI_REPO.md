## EPEL Repository và REMI Repository


### 1. EPEL Repository
Extra Packages for Enterprise Linux Là một kho chứa chương trình cộng đồng mở và miền phí được Fedora phát triển và duy trì. Cung cấp các gói phần mềm, chương trình chất lượng cao dành cho hệ điều hành Linux như Redhat, CentOS, Fedora,....

Hiểu đơn giản là REPO gần giống với CHplay hay App Store, chỉ cần cài đặt chúng lên hệ điều hành của mình thì hệ thống sẽ tìm các gói packages mà bạn muốn download thông qua lên Yum một cách dễ dàng.

#### 1.1 Cài đặt 
- C1: Cài đặt thông qua lệnh yum
Đơn giản, nhanh chóng.

`yum install epel-release`

- C2: Cài đặt thông qua lệnh rpm

`rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-7.noarch.rpm`

Hoặc: 

`rpm -ivh http://dl.fedoraproject.org/pub/epel/epel-release-7.noarch.rpm`

Cách 3: Cài đặt thông qua lệnh wget và rpm
`wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && rpm -Uvh epel-release-latest-7*.rpm`

Nếu bạn không sử dụng được lệnh wget thì có thể bạn chưa cài đặt packages. Lúc này chỉ cần dùng lệnh sau:
`yum install wget -y`

- Kiểm tra EPEL đã được cài đặt chưa

File cấu hình của EPEL nằm trong file `/etc/yum.repos.d/epel.repo`

Mặc định thì CentOS/RedHat sẽ sử dụng mặc định repo EPEL.

#### 1.2. Xóa 

- Xóa 

`yum remove epel-release`

- Xóa EPEL nếu cài đặt thông qua `rpm`

Tìm EPEL package
```
rpm -qa | grep epel
epel-release-7-11.noarch
```

- Xóa package bằng `rpm-e`

`rpm -e epel-release-6-8.noarch`

### 2. REMI REPO

REMI cũng tương tự như EPEL nhưng được đón nhận nhiều hơn vì thường cung cấp các gói packages mới nhất và nhanh hơn so với EPEL

Cài repo Remi chỉ nhằm hỗ trợ cho bạn thêm nhiều kho chứa các packages mới mà thôi, chính vì vậy các bạn nên cài đặt các repo EPEL trước khi cài đặt repo của REMI.Trong Fedora, nó dược bật theo mặc định, nhưng trong Centos và RHEL 7, bạn sẽ cần phải lm: 

### 2.1. Cài đặt: 

- `yum install epel-release`

- `yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm` #CentOS/RHEL 7

Hoặc : `#wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm `

`rpm -i remi-release-7*.rpm`

Hoặc: `rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm`

### 2.2. Kích hoạt

Mặc định, Remi không được kích hoạt. 

- Để kích hoạt tạm thời. 

`yum --enablerepo=remi install package`

- Để kích hoạt vĩnh viễn: **/etc/yum.repos.d/remi.repo**

Thay đổi: **enabled=0** thành **enabled=1**. 

Xóa Remi: 
`yum remove epel-release`
