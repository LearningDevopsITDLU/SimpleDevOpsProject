# Create a First Maven Jenkins job to build hello-world project 
# *Jenkins Job name:* `My_First_Maven_Build`

Chúng ta biết cách sử dụng các công cụ Git, Jenkins một cách độc lập. Nếu kết hợp 2 công cụ này thì bạn sẽ nghĩ như thế nào, điều này có thể giúp bạn tạo nên một quy trình CI và cũng chính là công việc của kỹ sư DevOps.

#### Điều kiện cần để triển khai:

1. Jenkins server 

### Các bước tạo "My_First_Maven_Build" Jenkin job
1. Đăng nhập Jenkins console
1. Create *Jenkins job*, Fill the following details,
   - *Source Code Management:*
      - Repository: `https://github.com/yankils/hello-world.git`
      - Branches to build : `*/master`  
   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`