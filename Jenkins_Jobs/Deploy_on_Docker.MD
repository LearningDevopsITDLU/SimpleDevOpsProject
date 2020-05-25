# Deploy lên Docker host server sử dụng Jenkins 
# *Jenkins Job name:* `DeployOnDockerHost`

### Điều kiện triển khai:

1. Jenkins server 
1. Docker-host Server 

### Tích hợp Docker-host và Jenkins

Cài đặt "publish Over SSH"
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `Publish over SSH`

Kết nối giữa Docker-host và Jenkins

- `Manage Jenkins` > `Configure System` > `Publish Over SSH` > `SSH Servers` 

	- SSH Servers:
                - Name: `docker-host`
		- Hostname:`<ServerIP>`
		- username: `dockeradmin`
               
       -  `Advanced` > chose `Use password authentication, or use a different key`
		 - password: `*******`
 
### Các bước tạo công việc "DeployOnDockerHost" bằng Jenkins
 #### From Jenkins home page select "New Item"
   - Nhập tên: `DeployOnDockerHost`
     - Copy from: `DeployOnTomcatServer`
     
   - *Source Code Management:*
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
	 

Save and run the job now. (Lưu và chạy công việc của bạn)