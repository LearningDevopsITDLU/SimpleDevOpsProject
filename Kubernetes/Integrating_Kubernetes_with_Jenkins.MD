## Tích hợp Kubernetes vào Jenkins để thực thi các quy trình Ci/CD

# *Jenkins CI Job:* `ContinuousIntegration_Final`

### Môi trường yêu cầu

1. Jenkins server 
1. Ansible server
1. Kubernetes cluster
 
### Các bước cấu hình "ContinuousIntegration_Final" để tạo quy trình CI cho Jenkins
#### Ở trang home page của Jenkins chọn "New Item"
   - Thêm vào tên của công việc `ContinuousIntegration_Final`
     - Copy from: `DeployOnDockerContainerUsingAnsible`
     
   - *Source Code Management:*
      - Repository: `https://github.com/LearningDevopsITDLU/hello-world`
      - Branches to build : `*/master`  
   - *Poll SCM* :      - `* * * *`

   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`

 - *Post-build Actions*
   - Send build artifacts over SSH
     - *SSH Publishers*
      - SSH Server Name: `ansible server`
       - `Transfers` >  `Transfer set`
           - Source files: `webapp/target/*.war`
	       - Remove prefix: `webapp/target`
	       - Remote directory: `//opt/CICDProject-Final`
	       - Exec command: 
                ```sh 
                ansible-playbook -i /opt/CICDProject-Final/hosts /opt/CICDProject-Final/create-simple-devops-image.yml;
                ```

Save and run công việc này để hoàn thành quy trình CI.

# *Jenkins CD Job:* `ContinuousDeployment_Final`

### Các bước cấu hình "ContinuousIntegration_Final" để tạo quy trình CD cho Jenkins
#### Ở trang home page của Jenkins chọn "New Item"
   - Thêm vào tên của công việc: `ContinuousIntegration_Final`
     - Freestyle Project
	 
  - *Post-build Actions*  
    - Send build artifacts over SSH  
      - *SSH Publishers*  
	       - Exec command: 
                ```sh 
                ansible-playbook -i /opt/CICDProject-Final/hosts /opt/CICDProject-Final/kubernetes-devopsitdlu-deployment.yml;
                ansible-playbook -i /opt/CICDProject-Final/hosts /opt/CICDProject-Final/kubernetes-devopsitdlu-service.yml
                ```
Lưu là chạy công việc này (Save and Build).
