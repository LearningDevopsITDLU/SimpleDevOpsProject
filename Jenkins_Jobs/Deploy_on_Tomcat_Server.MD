# Deploy lên a Tomcat server
# *Jenkins Job name:* `DeployOnTomcatServer`

### Điều kiện triển khai

1. Jenkins server 
2. Tomcat Server 

### Các bước triển khai

1. Cài đặt 'deploy to container' plugin. Plugin này cần thiết để deploy tập tin war lên tomcat server. 

  - Cài đặt 'deploy to container' plugin without restart  
    - `Manage Jenkins` > `Jenkins Plugins` > `available` > `deploy to container`
 
2. Jenkins cần truy cập vào máy chủ tomcat để triển khai các tập tin war. Thiết lập thông tin đăng nhập để cho phép quá trình đăng nhập này. Sử dụng tuỳ chọn thông tin đăng nhập trên trang chủ Jenkins.

- setup credentials
  - `credentials` > `jenkins` > `Global credentials` > `add credentials`
    - Username	: `deployer`
    - Password : `deployer`
    - id      :  `deployer`
    - Description: `user to deploy on tomcat vm`

### Các bước tạo "DeployOnTomcatServer" Jenkin job
 #### From Jenkins home page select "New Item"
   - Nhập tên: `Deploy_on_Tomcat_Server`
     - Copy from: `My_First_Maven_Build`
     
   - *Source Code Management:*
      - Repository: `https://github.com/yankils/hello-world.git`
      - Branches to build : `*/master`  
   - *Poll SCM* :      - `* * * *`

   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`

 - *Post-build Actions*
   - Deploy war/ear to container
      - WAR/EAR files : `**/*.war`
      - Containers : `Tomcat 8.x`
         - Credentials: `deployer` (user created on above)
         - Tomcat URL : `http://<PUBLIC_IP>:8080`

Save and run the job now. (Lưu và chạy công việc của bạn)