# Package management in Linux

## Package là gì ?
- Package được hiểu là tập hợp tất cả các files, metadata và các thông tin được hệ điều hành sử dụng để chạy một software application. Với các distros của Linux, ta có thể dùng các packages để cài đặt, bảo trì các phần mềm.
- Vì mỗi thiết bị chạy Linux lại có một kernel khác nhau, nên không thể đảm bảo được việc một chương trình Linux có thể chạy được trên tát cả các thiết bị chạy Linux. Vì vậy, package ra đời để giải quyết việc như vậy. Trong package có các **dependencies** tức là danh sách các thư viện, phần mềm cần phải có trước khi cài đặt một phần mềm.
### Các loại Packages trong Linux:
1. Distro-native Package:
   - Là các packages có được quản lý bởi các package manager như là **apt**, **yum**, **dnf**.Thông thường Distro-native Package sẽ có 2 loại chính đó là:
     - Debian Packages: thường được sử dụng ở những bản phân phối Linux được xây dựng dựa trên Debian và có đuôi **.deb** ở mỗi packages. Các dependencies trong Debian Packages được quản lý với các package managers như là **apt**, **apt-get**
     - RPM Packages: Các packages này thường được sử dụng trên các bản phân phối Linux được xây dựng dựa trên RedHat và có đuôi **.rpm**. Các dependencies trong RPM Packages được quản lý với các package managers như là **Yum** và **Dnf**.
2. Containerized Package: 
   - Là các package chứa các dependencies và ứng dụng được đóng gói trong một container có thể chạy độc lập trên nhiều môi trường khác nhau mà không bị conflict với cấu hình mặc định của hệ thống. 
   - Các containerized package phổ biến:
     - Snap: gồm ứng dụng và các dependencies của ứng dụng đó được đóng gói lại để có thể chạy trên nhiều các hệ điều hành Linux khác nhau. Snap có một centralized repos là **Snap Store** nơi lưu trữ tất cả các package. Snap Store giúp user có thể tìm và cài đặt các ứng dụng.
     - AppImage: AppImage là một executable file tương tự với file **.exe** ở Windows. Người dùng không cẩn phải cài đặt AppImage. AppImage dùng để chuyển 1 ứng dụng và các dependencies của nó thành một file duy nhất.
     - Flatpak tương tự như Snap cũng thực hiện đóng gói ứng dụng và các dependencies tương ứng vào trong một container để dễ dàng chạy một cách an toàn mà không phụ thuộc vào cài đặt của hệ thống. Ngoài ra Flatpak còn có khả năng tự động cập nhật ứng dụng từ kho lưu trữ riêng khiến cho người dùng luôn được sử dụng phiên bản mới nhất và an toàn nhất.

## YUM và APT: 
### Repository là gì ?
- Repository là được hiểu là kho chứa các software package có sẵn. Repo được chia ra làm 3 loại:
    + Local repo: là repo có sẵn ở trong máy local.
    + Centralized Internal repo: là repo được lưu ở một server trên mạng LAN, chưa một hoặc nhiều các packages.
    + Vendor repo: Là các repo có trên Internet, được sở hữu bới các distribution vendor.
### YUM:
- **rmp**: là một phiên bản cấp thấp dùng để quản lý các package cho những hệ điều hành Linux được xây dựng bởi RedHat. rmp có tác dụng cài đặt, gỡ cài đặt với các software package có đuôi **.rmp** 
   - Các options hay dùng khi sử dụng rmp:
     Options| Mục đích
     ---|---
     `-i {package name}`| Cài đặt package. 
     `-e {package name}`| Xóa hoặc gỡ cài đặt package.
     `-v`| bật verbose mode để cung cấp thêm thông tin về package.
     `-V {package name}`| Xác nhận rằng những thành phần của package đó có sẵn.
   - Ngoài ra còn có các câu lệnh hỗ trợ phổ biến khác như là:
     Câu lệnh| Mục đích 
     ---|---
     `rpm -qa {package name}`| List tất các các phần mềm đã được cài đặt.
     `rpm -qi {package name}` | List những thông tin về package.
     `rpm -qf {path/to/file}`| Tìm package mà file đó thuộc về.
     `rpm -ql {package name}` | Liệt kê các file thuộc package đó.
     `rpm -qc {package name}` | List những file cấu hình của package.

- YUM (Yellowdog Updater Modified): là một package manger phiên bản nâng cấp hơn của rmp được sử dụng cho những hệ điều hành Linux được xây dựng bởi RedHat. YUM là một ứng dụng front-end để quản lý các RPM package (quản lý các package có đuôi **.rpm**) có ở trong các repos. 
- Quản lý các package trong YUM:
   - Có rất nhiều các options và các command có sẵn được sử dụng với YUM. Sau đây là một số các command thông dụng và hay được sử dụng với YUM:
    
      ``` 
       yum -option command {package name}
      ```

    Command| Mục đích
    ---|---
    `yum install {package name}`| Dùng để cài đặt các package có sẵn từ các repo.
    `yum localinstall {package name}`| Dùng để cài đặt các package từ local repo.
    `yum search {package name}` | Dùng để tìm kiếm các thông tin về package theo từ khóa.
    `yum info` | Liệt kê các thông số của package.
    `yum update` | Cập nhật các package đến phiên bản mới nhất.
    `yum provides {file name}` | Xem file hoặc thư viện này thuộc package nào.
    `yum history` | Dùng để xem lại thông tin của các lần thực hiện trước.Ví dụ như là ngày tháng cài đặt, xóa các package.
    `yum upgrade` | Một phiên bản rộng hơn của update có thể cập nhật tất cả package đã được cài đặt cũng như các ứng dụng cảu hệ thống. 


    Options| Mục đích:
    ---|---
    `-y`| Tự động trả lời có để cài đặt các additional software dependencies. 
    `--skip-broken`| Bỏ qua các packages mà bị lỗi.
    `-V`| Sử dụng chế độ Verbose.
    `-C` | Chạy từ system cache.

- Ngoài ra còn có một công cụ quản lý package tương tự với `yum` và `rpm` đó là **dnf**. **dnf** hỗ trợ rpm, sử dụng ít tài nguyên hơn với những tính năng tương tự để quản lý các package như là cài đặt, gỡ cài đặt các package,.....

  - Cấu trúc câu lệnh của dnf là: 
    ```
      dnf [command] [file name]
    ```     
  - Để xem chi tiết hơn về dnf sử dụng `man dnf`.
 
