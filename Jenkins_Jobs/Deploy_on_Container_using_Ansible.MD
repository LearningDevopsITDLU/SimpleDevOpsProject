# Triển khai war file trên docker container sử dụng Ansible
# *Jenkins Job name:* `DeployOnContainerUsingAnsible`

### Điều kiện cần triển khai:

1. Jenkins server 
1. Docker-host server 
1. Ansible server
1. `Dockerfile` được lưu trong đường dẫn thư mục *`/home/dockeradmin`*
   ```sh 
   # Pull tomcat latest image from dockerhub 
   From tomcat
   # Maintainer
   MAINTAINER "ManhHa ITDLU" 

   # copy war file on to container 
   COPY ./webapp.war /usr/local/tomcat/webapps

1. Tạo `create-docker-image.yml` 
   ```ssh
   ---
   - hosts: all
     become: ture

     tasks:
     - name: creating docker image using docker command
       command: docker run -d --name simple-devops-container -p 8080:8080 simple-devops-image
   ```

### Tích hợp Ansible-control và Jenkins

Cài đặt "publish Over SSH"
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `Publish over SSH`

Kết nối giữa Ansible-control-node and Jenkins

- `Manage Jenkins` > `Configure System` > `Publish Over SSH` > `SSH Servers` 

	- SSH Servers:
                - Name: `ansible-server`
		- Hostname:`<ServerIP>`
		- username: `ansadmin`
               
       -  `Advanced` > chose `Use password authentication, or use a different key`
		 - password: `*******`
 
### Các bước tạo "DeployOnContainerUsingAnsible" Jenkins
#### Tại trang chủ Jenkins chọn "New Item"
   - Nhập tên: `Deploy_on_Container_using_ansible`
     - Copy from: `Deploy_on_Container`
     
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
      - SSH Server Name: `ansible-server`
       - `Transfers` >  `Transfer set`
            - Source files: `webapp/target/*.war`
	       - Remove prefix: `webapp/target`
	       - Remote directory: `//opt//docker`
	       - Exec command: 
                ```sh 
                ansible-playbook -i /opt/docker/hosts /opt/docker/create-docker-image.yml;
                ```

Save and run the job now. (Lưu và chạy công việc của bạn)
