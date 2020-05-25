# Cấu hình Git plugin trên Jenkins
 
Git là một trong những công cụ phổ biến nhất cho hệ thống quản lý phiên bản. Bạn có thể lấy mã nguồn (pull) từ kho chứa Git bằng Jenkin nếu bạn sử dụng plugin GitHub.

#### Prerequisites
1. Jenkins server 

#### Install Git on Jenkins server
1. Install git packages on jenkins server
   ```sh
   yum install git -y
   ```

#### Setup Git on jenkins console
- Install git plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `github`

- Configure git path
  - `Manage Jenkins` > `Global Tool Configuration` > `git`

