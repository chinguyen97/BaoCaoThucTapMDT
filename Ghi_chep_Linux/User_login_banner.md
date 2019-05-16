### User login Banner

### 1. Hiển thị banner trước đăng nhập:  

- B1: Edit file `/etc/issue.net` . Add message and save file. 

- B2: Edit file `/etc/ssh/sshd_config`

Thêm hoặc sửa dòng có chữ Banner : `Banner /etc/issue.net`

- B3: Restart sshd

`systemctl restart shhd`

- B4: Check

### 2. Hiển thị banner sau đăng nhập: 

Edit file `/etc/motd`

Thực hiện tương tự

### 3. Bạn cũng có thể tạo 1 fiel riêng và trỏ nó đến dường dẫn đó

- B1: Tạo 1 file login banner 
`# vi /etc/ssh/sshd-banner`
- B2: Mở file caaus hinhf sshd
`vi /etc/ssh/sshd_config`
- B3: Add/edit fiel
`Banner /etc/ssh/sshd-banner`
- B4: Saved file và khởi động lại dịch vụ
`systemctl restart sshd`
- B5: Test

***Tài liệu tahm khảo***: https://www.tecmint.com/protect-ssh-logins-with-ssh-motd-banner-messages/