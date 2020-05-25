# Cài đặt Ansible

Ansible là một nền tảng mã nguồn mở hỗ trợ tự động hoá với những thiết lập đơn giản nhưng rất mạnh mẽ. Ansible có thể giúp bạn quản lý cấu hình, triển khai ứng dụng - dịch vụ và tự động hoá tác vụ.

### Điều kiện cần để triển khai

1. Một máy ảo EC2 của AWS (An AWS EC2 instance)

### Các bước cài đặt:
#### Trên máy ảo EC2 AWS

1. Cài đặt python và python-pip
   ```sh
   yum install python
   yum install python-pip
   ```
1. Cài đặt ansible bằng cách sử dụng pip để kiểm tra phiên bản
    ```sh
    pip install ansible
   ansible --version
   ```
   
1. Tạo người dùng được gọi là ansadmin (đối với Control node và Managed host)  
   ```sh
   useradd ansadmin
   passwd ansadmin
   ```
1. Dưới đây là lệnh cấp quyền truy cập sudo cho user ansadmin. Có 2 cách để thực hiện là: sử dụng lệnh "visudo" nếu bạn có thể sử dụng được các trình soạn thảo "vi" hoặc "nano" (Đối với Control node và Managed host)
   ```sh
   echo "ansadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
   ```
   
1. Đăng nhập với người dùng ansadmin và tạo khoá ssh (Đối với Control node)
   ```sh 
   sudo su - ansadmin
   ssh-keygen
   ```
1. Copy khoá đến tất cả máy được quản lý bởi ansible (Đối với Control node)
   ```sh 
   ssh-copy-id ansadmin@<target-server>
   ```

1. Máy chủ Ansible được sử dụng để tạo images và lưu trữ images tại docker registry. Do đó chúng ta cần cài đặt Docker, bắt đầu sử dụng dịch vụ Docker và thêm user ansadmin vào nhóm Docker. 
   ```sh
   yum install docker
   
   # start docker services 
   service docker start
   service docker start 
   
   # add user to docker group 
   usermod -aG docker ansadmin

   ```
1. Tạo thư mục /etc/ansible và tạo một tập tin có tên là "hosts" để thêm các node được điều khiển bởi Ansible và quản lý địa chỉ IP được lưu trữ trong tập tin.
 
### Kiểm tra kết nối

   
1. Chạy lênh ansible với người dùng admin.
   ```sh 
   ansible all -m ping
   ```
