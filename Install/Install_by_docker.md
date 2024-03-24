# Cài đặt PostgeSQl sử dụng Docker

```
docker run --name <container_name> -e POSTGRES_USER=<postgre_user> -e POSTGRES_PASSWORD=<postgre_password> -p 5432:5432 -v <mount_folder>:/var/lib/postgresql/data -d postgres:<tag>
```

Trong đó:

--name <container_name> là tên Docker container mà các bạn muốn đặt cho container của PostgreSQL server.

-e POSTGRES_USER=<postgre_user> khai báo biến môi trường POSTGRES_USER, là tên user mà chúng ta sẽ sử dụng để đăng nhập vào PostgreSQL service. Tham số này là optional, nếu các bạn không khai báo thì mặc định, user với username “postgres” sẽ được sử dụng.

-e POSTGRES_PASSWORD=<postgre_password> là mật khẩu để đăng nhập với username ở trên. Tham số này là bắt buộc các bạn nhé!

-v <mount_folder>:/var/lib/postgresql/data giúp chúng ta mount một thư mục trên máy cài Docker với thư mục /var/lib/postgresql/data của PostgreSQL server, giúp chúng ta có thể synchronize data của PostgreSQL server trong container lên máy cài Docker, phòng trường hợp Docker Container của chúng ta có vấn đề gì, có thể chạy lại mà không mất dữ liệu.

-d là tham số giúp chúng ta chạy câu lệnh trong background, giúp chúng ta có thể tiếp tục container khi tắt Terminal hoặc Ctrl+C.

-postgres:<tag> là tag Docker Image của PostgreSQL server mà các bạn muốn chạy.

```
docker run --name postgresql -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=123456 -p 5432:5432 -v /opt/postgresql/data:/var/lib/postgresql/data -d postgres:13.3
```




