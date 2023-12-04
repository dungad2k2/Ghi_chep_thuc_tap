# System startup and shutdown

## Boot process
### Các khái niệm:
- Booting là chỉ sự hoạt động của 1 tiến trình khi tiến hành khởi động hoặc restart một máy tính cũng như tải một hệ điều hành.
- Boot loader là một chương trình nhỏ được lưu ở trong ROM thực hiện nhiệm vụ tải lên kernel từ một thiết bị lưu trữ, boot loader bảo vệ quá trình boot bằng một mật khẩu.
- Boot loader bao gồm 3 thành phần:
1. Boot sector program: có nhiệm vụ chính là khởi động quá trình boot của hệ thống. Khi bật máy tính, boot sector đầu tiên sẽ được tải từ ổ cứng hoặc ổ đĩa. Boot sector chứa các hướng dẫn cần thiết để khởi động hệ điều hành.
2. Second Stage Boot Loader: là một phần mở rộng của boot sector ban đầu, sau khi boot sector hoàn thành việc khởi động ban đầu, second stage boot loader sẽ thực hiện việc nạp hệ điều hành, khởi động hệ điều hành.
3. Boot Loader Installer: là công cụ hoặc chương trình được sử dụng để cài đặt boot loader vào máy tính, giúp cài đặt boot loader vào vị trí đúng đắn trên ổ đĩa cứng và cấu hình nó để khởi động hệ điều hành.
### Các options khi boot hệ điều hành:
1. **BIOS**(Basic input output system): là một firmware thường được nằm trên ROM của bo mạch chủ, cung cấp các cách thức để hoạt động và tương tác giữa phần cứng và phần mềm trong máy tính.
2. **UEFI**(Unified Extensible Firmware Interface): là một firware mới thay thế cho BIOS truyền thống. UEFI cung cấp nhiều tính năng hơn so với Bios như là: cung cấp GUI, có khả năng mở rộng, bảo mật,....
- Ngoài ra còn có các Boot options khác như là từ file `.iso` image là boot từ Network File System.
### Quá trình boot trong linux:
![](image/Linux-boot-process.png)
- Quá trình boot của hệ điều hành linux được thể hiện bên trên bao gồm các bước:
1. **Power On**: thực hiện cấp nguồn điện cho các thiết bị trong máy tính.
2. POST(Power-on-Self-Test): các thiết bị trong máy tính sẽ tự kiểm tra xem nguồn điện vừa được cấp có phù hợp không
3. **BIOS**: Thực hiện nhiệm vụ xác nhận tất các các thành phần được gắn và xác định thứ tự boot của các thiết bị, dựa vào thứ tự đó mà BIOS sẽ thực hiện boot cái gì trước.
![](image/Boot-Device-Order.png)
4. **MBR**(Master Boot Record): bao gồm boot loader, thông tin về partition và magic blocks  thường có kích thướng là 512 byte. Trong đó: 446 byte được cấp cho phần boot loader, 64 byte là thông tin về partition sẽ cung cấp hoặc chuyển hướng đến phân vùng `/boot` để tìm GRUB2.
5. **GRUB**(Grand Unified Boot Loader): là một file cấu hình được đặt ở `/boot/grub2/grub.cfg` thực hiện chỉ đến **initramfs**. Initramfs sẽ tải các block device drivers như là SATA, RAID,... Initramfs là phần bao bên ngoài của kernel, và kernel được mount đến initramfs.
6. **Kernel**: GRUB2 sẽ gọi đến boot menu khi quá trình boot được tiến hành và kernel sẽ được tải. Khi Kernel tải thành công nó sẽ lập tức tiến hành các tiến trình và dịch vụ khác.
7. **Khởi động Systemd-tiến trình đầu tiên của hệ thống**: Khi systemd được khởi tạo nó thực hiện khởi động tất các system service. Trước systemd sẽ không có các tiến trình nào khác, systemd được khởi động bằng cách gọi hàm `fork()`, hệ thống fork sẽ gán PID cho systemd là 1. Systemd được khởi chạy ở thư mục `/etc/systemd/systemd/default.target`. 
8. **Thực hiện khởi động các serive trong default.target**: các service khác sẽ được khởi động lần lượt theo thứ tự ở trong default.target, càng nhiều service thì quá trình khởi động càng chậm.
- Để xem được quá trình khởi động mất bao lâu ta thực hiện:
  ```
    sudo systemd-analyze time
  ```
  ![]()

- 