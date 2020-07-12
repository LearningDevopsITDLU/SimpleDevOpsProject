# Tích hợp Kubernetes cluster với Ansible

1. Login vào Ansible Server và copy public key đến các Kubernetes cluster 

1. Cập nhật file hosts với group có tên kubernetes và thêm địa chỉ IP Public của máy Kubernetes master. 

1. Tạo Ansible playbook để tạo ra một công việc đại diện cho việc triển khai **[deployment](https://github.com/LearningDevopsITDLU/SimpleDevOpsProject/blob/master/Kubernetes/kubernetes-itdlu-deployment.yml)** và dịch vụ **[services](https://github.com/LearningDevopsITDLU/SimpleDevOpsProject/blob/master/Kubernetes/kubernetes-valaxy-service.yml)** 
		
1.  Kiểm tra pods, deployment và services trên Kubernetes master bằng lệnh
    ```sh 
    kubectl get pods -o wide 
    kubectl get deploy -o wide
    kubectl get service -o wide
    ```
	
1. Truy cập vào ứng dụng đang được triển khai với địa chỉ IP và Port cấu hình cụ thể
   ```sh
   wget <kubernetes-Master-IP>:30003
   ```
