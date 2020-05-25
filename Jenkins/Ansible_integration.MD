# Tích hợp Ansible với Jenkins

### Part-01 Các bước tích hợp.

Cài đặt "publish Over SSH"
 - `Manage Jenkins` > `Manage Plugins` > `Available` > `Publish over SSH` 

Cho phép kết nối giữa Ansible và Jenkins.
- `Manage Jenkins` > `Configure System` > `Publish Over SSH` > `SSH Servers` 

	- SSH Servers:
		- Hostname:`<ServerIP>`
		- username: `ansadmin`
		- password: `*******`

Kiểm tra kết nối "Test Connection"
