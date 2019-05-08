## LINUX PID 1 & SYSTEMD

Để nói Systemd, bạn phải bắt đầu với việc khởi động hệ điều hành LINUX. Việc khởi động HĐH Linux bắt đầu bằng BIOS, sau đó kernel được tải bởi Boot Loader và kernel được khởi tạo. Bước cuối cùng trong khởi tạo kernel là bắt đầu tiến trình init. Tiến trình này là tiến trình đầu tiên của hệ thống, PID là 1, hay còn gọi là siêu tiến trình, hay tiến trình gốc. Nó chịu trách nhiệm tạo ra tất cả cac stieens trình của người dùng khác. Nếu tiến trình này thoát tất cả các tiến trình khác sẽ bị hủy. (PID 0 là 1 phần của nhân chứ không phải 1 tiến trình người dùng)

### 1. SysV Init
PID 1 là quá trình đặc biệt, tác vụ chính đưa toàn bộ hệ thống vào trạng thái hoạt động. Ví dụ: Khởi chạy UI-Shell để tương tác vpsi người dùng thông qua giao diện đồ họa X. Theo truyền thống, PID 1 tương tác với Unix System V truyền thống, do đó còn được gọi là sysvinit, nó là init triển khai lâu đời nhất. Unit System V được phát hành năm 1983.

Trong SysV init, có 1 số phương thức hoạt động được gọi là runlevel. Ví dụ: Level 3: bắt đầu giao diện dòng lệnh với nhiề người dùng. Level 5: Bắt đầu gao diện đồ họa, 0: tắt máy, 6 khởi động lại.Trong File cấu hình `/etc/inittab`

Gói này có `/etc/init.d` và `/etc/rc[X].d` lưu trữ các quá trình bắt đầu và ngừng các tiến trình (theo thông số kỹ thuật hỗ trợ các lệnh cần thiết start, stop), X đại diện cho các runlevel khác nhau, chẳng hạn `/etc/rc3.d` là runlevel 3. các tập tin bên trong `/etc/init.d` là tập các lệnh bắt đầu và dừng liên kết. Có 1 số quy ước đặt tên: bắt đầu với K hoặc S, tiếp theo là các con số, sau đó đến các tùy chỉnh, chẳng hạn như `S01rsyslog`, `S02ssh`. S có nghĩa là bắt đầu, K có nghĩa là dừng và các số chỉ thứ tự thực hiện.

### 2. UpStart 

Sysvinit hoạt động nhiều năm trên HĐH unix và Linux, đến khoảng năm 2006, Linux kernel vào thời đại 2.6, Linux có nhiều cập nhật. Hơn nữa Linux bắt đầu xuất hiện trong trong hệ thống máy tính để bàn, và hệ thống máy chủ khác. Hệ thống máy tính để bàn thường xuyên được khởi động lại và người dùng sử dụng công nghệ cắm nóng phần cứng thường xuyên. Vì vậy sysvnit có nhiều thách thức. 

Ví dụ: Máy in cần 1 quy trình dịch vụ như CUPS, nếu như người dùng không có máy in thì việc khởi động lại dịch vụ gây lãng phí, nếu không được khởi động, nếu máy in được sử dụng, nó sẽ không thể sử dụng được vì sysvint không có cơ chế phát hiện tự động. Có thể bắt đầu tất cả cac sdichj vụ cùng 1 lúc. Người ra còn 1 số vân sđề với việc gắn đĩa mạng. Trong `/etc/fstab` chứa các đĩa cứng để mount, vfa đôi kbi là 1 ổ đĩa mạng (NFS hoặc iCSI), nhưng trên máy tính để bàn, mạng không thể truy cập vào đĩa cứng, nó không có khả năng mount. Điều này ảnh hưởng đến tốc độ khởi động. SysVinit ắp dụng netdev để giải quyết vân sđề này, có nghĩa là nhu cầu của người dùng trong /etc/fstab cấu hình ổ cứng tương ứng với netdev, vì vậy SysVinit không gắn kết nó lúc khởi động, chỉ sau khi mạng có sẵn, bởi chuyên gia ngành netfs quá trình dịch vụ để miunt. Loai quản lý này khó quản lý hơn, và gây khó khăn cho mọi người. 

Vì vậy, các nhà phát triển Ubuntu đã quyết định thiết kế lại hệ thống sau khi đánh giá một hệ thống init tùy chọn tại thời điểm đó, vì vậy Upstart xuất hiện. Upstart dựa trên cơ chế hướng sự kiện, dịch vụ khởi động đồng bộ hoàn toàn nối tiếp trước đó đã được thay đổi bằng phương pháp không dồng bộ theo hướng sự kiện. Ví dụ: Nếu ổ flash USB được lắp vào, udev sẽ nhận được thông báo, upstart và chương trình dịch vụ tương ứng được kích hoạt sau khi sự kiện được cảm nhận, chẳng hạn như gán tệp hệ thóng. Do sử dụng dịch vụ hướng sự kiện, khi khởi động hệ điều hành, nhiều dịch vụ không cần thiết có thể được khởi động mà không phải chờ đợi. Và lợi ích của hướng sự kiện là các dịch vụ có thể được bắt đầu song song và các phụ thuộc giữa chúng được hoàn thành bằng thông báo sự kiện tương ứng.

Upstart có một thiết kế rất tốt, hai trong số đó quan trọng nhất là Công việc và Sự kiện.

Công việc có một công việc chung, một công việc dịch vụ và upstart quản lý vòng đời của toàn bộ công việc, như: Waiting, Starting, pre-Start, Spawned, post-Start, Running, pre-Stop, Stopping, Killed, post-Stop Wait và duy trì bộ máy trạng thái của vòng đời này.

Sự kiện được chia thành ba loại signal, method và hooks. signal Đó là một thông điệp đồng bộ, method đồng bộ bị chặn đồng bộ. hooks cũng đồng bộ, nhưng giữa hai lần đầu tiên, quá trình phát hành sự kiện hook phải đợi cho đến khi sự kiện hoàn thành, nhưng không kiểm tra thành công.

Tuy nhiên, upstart các sự kiện rất phức tạp và rất hỗn loạn, và các sự kiện khác nhau (các sự kiện không được phân loại) gây ra một chút nhầm lẫn. Tuy nhiên, do trước khi thiết kế toàn bộ event- driven của nó tốt hơn sysvinit nhiều do đó, cũng được chào đón.

###3. Systemd
Năm 2010, Lennart Poettering và Kay Sievers giới thiệu 1 init system mới: systemd. Đây là 1 dự án lớn, tham vọng đã thay đổi hầu hết mọi thứ, systemd không chỉ thay đổi hệ thống hiện tại mà nó còn làm được nhiều hơn thế nữa. 

Lennart đồng ý rằng upstart hoạt động tốt, chất lượng mã rất tốt, thiết kế dựa trên sự kiện cũng rất tốt. Tuy nhiên ông cảm thấy upstart có 1 số vấn đề, vấn đề lớn nhất là không đủ nhanh, mặc dù upstart đã đạt đến trình độ xử lý song song, nhưng bản chất các sự kiện này sẽ bắt đầu các quá trình nối tiếp nhau. Chẳng hạn như: NetworkManager chờ đợi sự kiện D-Bus bắt đầu, trong khi D-Bus chờ đợi sự kiện syslog bắt đầu.

Lennart tin rằng, về mặt triển khai, upstart thực sự đang quản lý cây phụ thuộc dịch vụ logic, nhưng cây phụ thuộc dịch vụ này tương đối đơn giản trong biểu thức. "Start B is good, start A" or "stop." After A, the rule of B" is stopped. Tuy nhiên, Lennart nói rằng sự đơn giản hóa này thực sự gây bất lợi. Ông tin rằng: 
- Từ quan điểm quản lý hệ thống, ông sẽ thiết lập cây phụ thuộc dịch vụ mà toàn bộ hệ thống bắt đầu lại từ đầu, nhưng quản trị viên hệ thống muốn chuyển đổi sạch dịch vụ ban đầu sang một máy tính. Biểu mẫu Event/Action và cấu hình Event/Action là thời gian chạy, vì vậy bạn cần chạy nó để biết nó là gì.
- Sự kiện logic ở khắp mọi nơi từ đầu đến cuối. Sự kiện này mở rộng sự phức tạp của vận hành và bảo trì, không còn tốt như trước sysvint. Đó là, khi bạn cấu hình "Start D-Bus Hãy start NetworkManager", điều này upstart có thể khô, nhưng ngược lại, nếu một người dùng bắt đầu NetworkManager, chúng ta nên đi để bắt đầu trước sự phụ thuộc của mình D-Bus, nhưng bạn phải cấu hình các sự kiện ngược lại. Ban đầu, tôi chỉ cần cấu hình một phụ thuộc và bây giờ tôi phải cấu hình nhiều sự kiện trong nhiều trường hợp.
- Cuối cùng, upstart Sự kiện không chuẩn, rất khó hiểu và không có định nghĩa tốt. Ví dụ: existing, process start, run, stop events, USB device insertion, usable, unplugged events, cũng như thiết bị hệ thống tệp được gắn, gắn và gắn các sự kiện, cũng như ngắt kết nối và ngắt kết nối dây nguồn AC Sự kiện. Bạn sẽ thấy rằng quá trình bắt đầu, dừng, USB, hệ thống tệp và đường dây nguồn trông rất giống nhau, nhưng nó không được chuẩn hóa, bởi vì hầu hết các sự kiện là ba lần: Start, condition, stop. Mô hình thiết kế khái niệm này và không có trong upstart xuất hiện. Do upstart được thiết kế để trở thành một sự kiện đơn, trong khi bỏ qua các phụ thuộc logic.

Tất nhiên, nếu systemd chỉ để giải quyết upstart vấn đề này, ông sẽ chuyển upstart đủ, nhưng Lennart tham vọng không chỉ muốn làm một điều như vậy, ông muốn làm nhiều hơn nữa.

Trước hết, tôi nhận ra rằng mục tiêu chính của systemd trong quá quá trình init là cho phép người dùng nhanh chóng xâm nhập vào môi trường nơi hệ điều hành có thể được vận hành. Do đó, tốc độ phải nhanh, càng nhanh càng tốt, vì vậy systemd khái niệm thiết kế là hai:
+ Để bắt đầu ít hơn
+ Để bắt đầu vào sâu hơn trong Parallel
Nghĩa là, bắt đầu theo yêu cầu, không thể bắt đầu mà không bắt đầu, nếu bạn muốn bắt đầu, bạn có thể bắt đầu song song và bắt đầu song song, bao gồm cả sự phụ thuộc giữa bạn, tôi cũng bắt đầu song song. Tốt hơn là nên hiểu về khởi động theo yêu cầu, sau đó, khởi động song song với các phụ thuộc, làm thế nào để làm điều đó? Ở đây, systemd dựa trên các trò chơi hệ điều hành MacOS Launchd được chơi (có được một chia sẻ trên Youtube , trong trang web mã nguồn mở của Apple cũng liên quan hồ sơ thiết kế - các Daemons và Services )

Để giải quyết các phụ thuộc này, systemd cần giải quyết ba phụ thuộc cơ bản - Ổ cắm, D-Bus và hệ thống tệp.

