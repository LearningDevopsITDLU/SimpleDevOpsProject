#  Cài đặt và cấu hình công cụ hỗ trợ xây dựng (build) Maven với Jenkins.

Maven là một công cụ xây dựng mã nguồn được sử dụng để chuyển đổi mã nguồn thành một tập tin được đóng gói. Đây là một plugin được sử dụng rộng rãi phục vụ giai đoạn Build trong quá trình Continuous Integration. 

#### Điều kiện
1. Jenkins server

#### Cài đặt Maven trên Jenkins
1. Tải về gói cài đặt Maven với đường dẫn: https://maven.apache.org/download.cgi onto Jenkins server. Đối với việc triển khai này, thư mục cài đặt Maven là: /opt/maven
 - Link : https://maven.apache.org/download.cgi
    ```sh
     # Tạo thư mục Maven
     mkdir /opt/maven
     cd /opt/maven
     # downloading maven version 3.6.0
     wget http://mirrors.estointernet.in/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
     tar -xvzf apache-maven-3.6.1-bin.tar.gz
     ```
	
1. Thiết lập M2_HOME và M2 paths trong .bash_profile  của user và thêm vào: 
  ```sh
   vi ~/.bash_profile
   M2_HOME=/opt/maven/apache-maven-3.6.1
   M2=$M2_HOME/bin
   PATH=<Existing_PATH>:$M2_HOME:$M2
   ```
#### Kiểm tra
1. Đăng xuất và đăng nhập lại để kiểm tra phiên bản Maven
  
    ```sh
    mvn --version
    ```
Đến đây, việc cài đặt công cụ Maven để hỗ trợ plugin Maven khi triển khai Jenkins. Tiếp theo là việc cài đặt Plugin:

### Thiết lập Maven tại Jenkins console
1. Cài đặt plugin Maven với tuỳ chọn không khởi động lại (Install maven plugin without restart)  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Invoker`
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

2. Cấu hình đường dẫn Maven
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`

