# Triển khai war file trên docker container sử dụng Jenkins 
# `DeployOnContainer`

### Điều kiện cần triển khai:

1. Jenkins server 
1. Docker-host server 
1. `Dockerfile` được lưu trong đường dẫn thư mục *`/home/dockeradmin`* 
   ```sh 
   # Pull tomcat image phiên bản mới nhất từ from dockerhub 
   From tomcat
   # Maintainer
   MAINTAINER "ManhHa ITDLU" 

   # copy war file on to container 
   COPY ./webapp.war /usr/local/tomcat/webapps

### Tích hợp máy chủ Docker-host vào Jenkins.

Cài đặt Plugin: "publish Over SSH"
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `Publish over SSH`

Kết nối giữa Docker-host và Jenkins

- `Manage Jenkins` > `Configure System` > `Publish Over SSH` > `SSH Servers` 

	- SSH Servers:
                - Name: `docker-host`
		- Hostname:`<ServerIP>`
		- username: `dockeradmin`
               
       -  `Advanced` > chose `Use password authentication, or use a different key`
		 - password: `*******`
 
### Các bước tạo công việc "DeployOnContainer" bằng Jenkins
#### Tại trang chủ Jenkins chọn "New Item"
   - Nhập tên: `DeployOnContainer`
     - Copy from: `DeployOnDockerHost`
     
   - Kết nối với GitHub *Source Code Management:*
      - Repository: `https://github.com/LearningDevOpsITDLU/hello-world.git`
      - Branches to build : `*/master`  
   - *Poll SCM* :      - `* * * *`

   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`

 - *Post-build Actions*
   - Send build artifacts over SSH
     - *SSH Publishers*
      - SSH Server Name: `docker-host`
       - `Transfers` >  `Transfer set`
            - Source files: `webapp/target/*.war`
	       - Remove prefix: `webapp/target`
	       - Remote directory: `//home//ansadmin` or `.`
	       - Exec command: 
                ```sh 
                cd /home/dockeradmin;
                docker build -t simple-devops-image .; 
                docker run -d --name simple-devops-container -p 8080:8080 simple-devops-image;
                ```

Save and run the job now. (Lưu và chạy công việc của bạn)
