#### Đối với RHEL 8.x server

1. Cài đặt Python phiên bản mới nhất (đối với Control node và Managed host)
   ```sh 
   yum install python3 -y
   ```

1. Mặc định, python3 là lệnh để chạy nhiều lệnh python khác nhau. Để chỉ sử dụng python, sử dụng lệnh "alternatives" (Đối với Control node và Managed host)
   ```sh 
   alternatives --set python /usr/bin/python3
   ```

1. Kiểm tra phiên bản Python  
   ```sh 
   python --version
   ```
1. Cài đặt gói quản lý python-pip (Đối với Control node)
   ```sh 
   yum -y install python3-pip
   ```

1. Tạo một user mới quản trị Ansible và gán quyền admin cho user này (đối với Control node và Managed host)
   ```sh 
   useradd ansadmin
   passwd ansadmin
   ```
1. Dưới đây là lệnh cấp quyền truy cập sudo cho user ansadmin. Có 2 cách để thực hiện là: sử dụng lệnh "visudo" nếu bạn có thể sử dụng được các trình soạn thảo "vi" hoặc "nano" (Đối với Control node và Managed host)
   ```sh
   echo "ansadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
   ```
1. Nên sử dụng xác thực dựa trên khoá (keys). (đối với Control node và Managed host)
   ```sh 
   # sed command replaces "PasswordAuthentication no to yes" without editing file 
    sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
    sudo service sshd reload
   ``` 

    #### Cài đặt Ansible với người dùng ansadmin (đối với Control node)
   ```sh 
   su - ansadmin
   pip3 install ansible --user
   ``` 
1. Kiểm tra phiên bản Ansible
   ```sh
   ansible --version
   ```

1. Đăng nhập với người dùng ansadmin và tạo khoá ssh (Đối với Control node)
   ```sh 
   ssh-keygen
   ```
1. Copy khoá đến tất cả máy được quản lý bởi ansible (Đối với Control node)
   ```sh 
   ssh-copy-id ansadmin@<target-server>
   ```
### Kiểm tra kết nối

1. Tạo thư mục /etc/ansible và tạo một tập tin có tên là "hosts" để thêm các node được điều khiển bởi Ansible và quản lý địa chỉ IP được lưu trữ trong tập tin.
   
1. Chạy lênh ansible với người dùng admin.
   ```sh 
   ansible all -m ping
   ```
