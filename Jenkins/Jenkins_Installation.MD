# Cài đặt Jenkins trên AWS EC2

Jenkins là một chương trình được viết bằng Java với các gói cài đặt cho Windows, Mac OS và các bản phân phối của hệ điều hành Linux. Là một máy chủ tự động hỗ trợ khả mở, Jenkins có thể được sử dụng như một máy chủ CI đơn giản hoặc đóng vai trò là trung tâm phân phối liên tục cho hỗ trợ CD cho các dự án.

### Điều kiện để thực hiện
1. EC2 Instance 
   - Đảm bảo kết nối Internet
   - Security Group với Port `8080` để truy cập Internet
1. Java v1.8.x 

## Cài đặt Java
1. Việc demo sẽ phát triển một dự án bằng ngôn ngữ java. Nên sử dụng phiên bản Java mới nhất từ url: http://openjdk.java.net/install/
   ```sh
   yum install java-1.8*
   #yum -y install java-1.8.0-openjdk-devel
   ```

1. Kiểm tra chính xác phiên bản Java và thiết lập thư mục làm việc Java
   ```sh
   java -version
   find /usr/lib/jvm/java-1.8* | head -n 3
   JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-<Java version which seen in the above output>
   export JAVA_HOME
   PATH=$PATH:$JAVA_HOME
    # Thiết lập Java Home bằng cách chỉnh sửa .bash_profile
   vi ~/.bash_profile
   ```
   _Kết quả sau khi thiết lập Java Home_
    ```sh
   [root@~]# java -version
   openjdk version "1.8.0_151"
   OpenJDK Runtime Environment (build 1.8.0_151-b12)
   OpenJDK 64-Bit Server VM (build 25.151-b12, mixed mode)
   ```

## Cài đặt Jenkins
 You can install jenkins using the rpm or by setting up the repo. We will set up the repo so that we can update it easily in the future.
1. Get the latest version of jenkins from https://pkg.jenkins.io/redhat-stable/ and install
   ```sh
   yum -y install wget
   sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
   sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
   yum -y install jenkins
   ```

   ### Khởi động Jenkins
   ```sh
   # Start jenkins service
   service jenkins start

   # Thiết lập Jenkins khởi động cùng hệ điều hành.
   chkconfig jenkins on
   ```

   ### Truy cập Jenkins
   Mặc định Jenkins sẽ chạy trên cổng `8080`, bạn có thể truy cập Jenkins với URL:
   ```sh
   http://YOUR-SERVER-PUBLIC-IP:8080
   ```
  #### Cấu hình Jenkins
- Mặc định user có username là `admin`
- Lấy mật khẩu mặc định 
- Mật khẩu mặc định sẽ được nằm trong file:`/var/lib/jenkins/secrets/initialAdminPassword`
- `Skip` Plugin Installation; _Bỏ qua bước cài đặt Plugin vì chúng ta sẽ cài từng plugin cụ thể đối với project_
- Thay đổi admin password
   - `Admin` > `Configure` > `Password`
- Cấu hình đường dẫn `java`
  - `Manage Jenkins` > `Global Tool Configuration` > `JDK`  
- Tạo thêm người dùng admin khác

### Bắt đầu với Jenkins Jobs
1. Create “new item” - Tạo mới một công việc
1. Nhập tên cho công việc – `MyFirstProject`
   - Chọn `Freestyle` project
1. Tại phần Build nhập lệnh:
	Execute shell: echo "Welcome to Jenkins Demo"
1. Lưu công việc đã thiết lập 
1. Build job
1. Kiểm tra kết quả thành công hay không ở "console output"

