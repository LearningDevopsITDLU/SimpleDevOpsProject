# Cài đặt Docker trên máy chủ Amazon Linux

### Điều kiện cần thiết
1. Amazon Linux EC2 Instance

## Các bước của quá trình cài đặt

1. Cài đặt Docker và khởi động dịch vụ Docker
   ```sh 
   yum install docker -y
   docker --version 
   
   # start docker services
   service docker start
   service docker status
   ```
1. Tạo user có tên dockeradmin
   ```sh
   useradd dockeradmin
   passwd dockeradmin
   ```
1. Thêm user này để quản lý group Docker 
   ```
   usermod -aG docker dockeradmin
   ```
### Kiểm tra và vận hành
1. Tạo một contaier docker tomcat bằng cách kéo image có phiên bản mới nhất
   ```sh
   docker run -d --name test-tomcat-server -p 8090:8080 tomcat:latest
   ```

## Cài đặt Docker trên CentOS server
##### URL tài liệu tham khảo : https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository
### Điều kiện cần thiết:

1. Cài đặt các gói cần thiết (required packages).

   ```sh 
   sudo yum install -y yum-utils \
   device-mapper-persistent-data \
   lvm2
   ```
  
1. Sử dụng những lệnh dưới để thiết lập một kho lưu trữ ổn định cho việc hoạt động.
 
   ```sh 
   sudo yum-config-manager \
   --add-repo \
   https://download.docker.com/linux/centos/docker-ce.repo
   ```

### CÀI ĐẶT DOCKER CE

1. Cài đặt phiên bản mới nhất của Docker CE.
   ```sh 
   sudo yum install docker-ce
   ```

   Lưu ý: Nếu nhận được yêu cầu sử dụng khoá GPG khớp với
060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35 và accept nó.

1. Khởi động Docker.
   ```sh 
   sudo systemctl start docker
   ```

1. Xác minh lại Docker được cài đặt chính xác hay chưa bằng cách chạy image hello-world
   ```sh
   sudo docker run hello-world
   ```
