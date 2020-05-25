## Docker Hub Registry là gì?

Docker Hub là một dịch vụ cho phép người dùng đăng kí và quản lý container được lưu trữ tại cloud. Docker Hub hỗ trợ người dùng liên kết với các container, xây dựng image và kiểm tra nó. Bên cạnh đó người dùng có thể lưu trữ images được đẩy thủ công và tạo liên kết với Docker Cloud để bạn có thể triển khai image đến máy chủ Docker của mình. Nó cung cấp một nguồn tài nguyên tập trung để lưu trữ, quản lý phân phối và thay đổi. Hỗ trợ cộng tác giữa người dùng và nhóm phát triển, tự động hoá quy trình làm việc trong suốt quá trình phát triển.

##### URL : https://docs.docker.com/docker-hub/

1. Tạo một tài khoản tại Docker Hub https://hub.docker.com/

1. Kéo về một image (Pull a docker image) 

   ```sh 
   docker pull ubuntu
   ```

1. Kéo về một image với phiên bản cũ tuỳ ý (pull a docker image with the old version)

   ```sh
   docker pull ubuntu:16.04
   ```

1. Tạo một thẻ tuỳ chỉnh cho Docker Image
   ```sh
   docker tag ubuntu:latest devops/ubuntu:demo
   ```

1. Đăng nhập vào Docker Hub 
   ```sh
   docker login
   docker push devops/ubuntu:demo
   ```

### Kiểm tra 

1. Xoá tất cả image tại máy chủ Docker 
   ```sh 
   docker image rm -f <Image_id>
   ```

1. Kéo image bạn đã tuỳ chỉnh từ tài khoản Docker Hub
   ```sh
   docker pull valaxy/ubuntu:demo
   ```

