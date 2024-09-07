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
4.  
