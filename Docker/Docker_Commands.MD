
1. Tìm một docker image tại hub.docker.com
```sh
docker search httpd
```
2. Download một docker image từ hub.docker.com
```sh
docker image pull <image_name>:<image_version/tag>
```

3. Liệt kê tất cả image trên hệ thống của bạn
```sh
docker image ls
```

4. Create/run/start một docker container từ image
```sh
docker run -d --name <container_Name> <image_name>:<image_version/tag>

d - chạy nền container của bạn - Run in background (detached)
```

5. Đưa ứng dụng của bạn đến máy chủ
```sh
docker run -d  -p <host_port>:<container_port> --name <container_Name> <image_name>:<Image_version/tag>

docker run -d --name httpd_server -p 8080:80 httpd:2.2
```

6. Liệt kê các container đang chạy
```sh
docker ps
```

7. Liệt kê các container (running, stpooed, terminated,...)
```sh
docker ps -a
```

8. Chạy một ứng dụng lên Container với image tương tác tuỳ ý

```sh
docker run -i -t --name centos_server centos:latest
i - interactive
t - Terminal
```

9. Dừng hoạt động của container 
```sh
docker stop <container_id>
```

10. Khởi động container đang ở trạng thái stop hoặc thoát ra

```sh
docker start <container_id>
```
11. Xoá (Huỷ bỏ) một container

```sh
docker rm <container_id>
```

12. Đăng nhập quản lý Docker Container
```sh
docker exec -it <container_Name> /bin/bash
```
