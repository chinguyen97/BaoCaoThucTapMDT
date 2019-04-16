### Thư mục trong linux, Socket

### 1. Folder 

Trong Linux thực chất không có khái niệm Folder. Mọi thứ trong Linux đều là File

Tệp thông thường -Là một tệp trên hệ thống chứa dữ liệu, văn bản hoặc hướng dẫn chương trình.
Thư mục - Thư mục lưu trữ cả các tập tin đặc biệt và thông thường. Đối với người dùng quen thuộc với Windows hoặc Mac OS, các thư mục Unix tương đương với các thư mục.

Các lệnh làm việc với thư mục: tạo, xóa, đổi tên, di chuyển.....

#### 2. Socket 

2 tiến trình/ 2 máy có để có thể giao tiếp với nhau ( gửi và nhận dữ liệu) cần thiết lập 1 kết nối=> Cần xây dựng 1 socket. Có thể hiểu socket giống như 1 điểm đầu cuối của kênh kết nối giữa 2 tiến trình. 

Socket là phương thức để giao tiếp giữa các tiến trình. Nghĩa là 1 socket được sử dụng để cho phép 1 process nói chuyện với 1 process khác. 

Trong quá trình làm việc các bạn có thể chạy nhiều socket cùng một lúc nên công việc của bạn sẽ nhanh hơn, nâng cao hiệu suất làm việc.

Điều kiện quan trọng nếu muốn thực hiện được kết nối này là các bạn phải biết số hiệu cổng socket và IP của một trong hai ứng dụng. Nếu kết nối hai ứng dụng của một hệ thống máy tính thì không được cùng một số hiệu cổng socket, nếu không hoạt động sẽ không được tiến hành.

Có 2 loại socket được sử dụng rộng rãi:
- Stream sockets: Dựa trên giao thức TCP (Tranmission Control Protocol), là giao thức hướng luồng (stream oriented). Việc truyền dữ liệu chỉ thực hiện giữa 2 tiến trình đã thiết lập kết nối. Giao thức này đảm bảo dữ liệu được truyền đến nơi nhận một cách đáng tin cậy, đúng thứ tự nhờ vào cơ chế quản lý luồng lưu thông trên mạng và cơ chế chống tắc nghẽn.
- Datagram sockets: Dựa trên giao thức UDP (User Datagram Protocol), là giao thức hướng thông điệp (message oriented). Việc truyền dữ liệu không yêu cầu có sự thiết lập kết nối giữa tiến quá trình. UDP không được tin cậy, có thế không đúng trình tự và lặp lại. Tuy nhiên vì nó không yêu cầu thiết lập kết nối không phải có những cơ chế phức tạp nên tốc độ nhanh…ứng dụng cho các ứng dụng truyền dữ liệu nhanh như chat, game….

