1. Chuẩn bị

2. Cài đặt PostgresSQL 13 trên 02 Node Ubuntu
```
#Add a GPG key
curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/apt.postgresql.org.gpg >/dev/null

#Add PostgreSQL repository on Ubuntu 22.04
echo "deb [arch=amd64] http://apt.postgresql.org/pub/repos/apt/ jammy-pgdg main" | sudo tee /etc/apt/sources.list.d/postgresql.list

#Rebuild APT index cache
sudo apt update

#Install PostgresSQL 13 on Ubuntu 22.04
apt install postgresql-13 postgresql-client-13
```

3. Sau khi cài đặt xong các đường dẫn sẽ như sau

```
File config: /etc/postgresql/13/main/

data_directory = '/var/lib/postgresql/13/main' 
hba_file = '/etc/postgresql/13/main/pg_hba.conf' 
ident_file = '/etc/postgresql/13/main/pg_ident.conf' 
external_pid_file = '/var/run/postgresql/13-main.pid'
stats_temp_directory = '/var/run/postgresql/13-main.pg_stat_tmp'
```
4.  Thay đổi đường dẫn mặc định

Tạo đường dẫn mới
```
mkdir -p /database/postgresql/13/
chown -R postgres:postgres /database/postgresql

su - postgres
mkdir -p  /database/postgresql/13/main
mkdir -p  /database/postgresql/13/logs
mkdir -p  /database/postgresql/13/archive
```

Thực hiện sửa đổi đường dẫn cấu hình mặc định file /etc/postgresql/13/main/postgresql.conf
```
data_directory = '/database/postgresql/13/main' 
```

Thực hiện stop database
```
systemctl stop postgresql@13-main.service
```

Chuyển dữ liệu từ /var/lib/postgresql/13/main sang /database/postgresql/13/main

```
sudo rsync -av /var/lib/postgresql/13/main /database/postgresql/13/
mv /var/lib/postgresql/13/main /var/lib/postgresql/13/main.bakyyyymmdd
```

Thực hiện start database
```
systemctl start postgresql@13-main.service
systemctl status postgresql@13-main.service
```

Check đường dẫn tiến trình
```
ps aux | grep postgres | grep -- -D

postgres  167951  0.0  0.0 218156 30764 ?        Ss   11:38   0:00 /usr/lib/postgresql/13/bin/postgres -D /database/postgresql/13/main -c config_file=/etc/postgresql/13/main/postgresql.conf
```


5.  
