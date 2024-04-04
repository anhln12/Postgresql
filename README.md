# postgresql

# Install PostgreSQL 9.6 in CentOS7
```code bash
sudo yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm -y
sudo yum install postgresql96 -y
sudo yum install postgresql96-server -y

sudo /usr/pgsql-9.6/bin/postgresql96-setup initdb
sudo systemctl enable postgresql-9.6
sudo systemctl start postgresql-9.6
```
# Edit pg_hba.conf file
```code bash
# You can get pg_hba.conf file location from postgreSQL console
postgres=# SHOW config_file;

sudo vim /var/lib/pgsql/9.6/data/pg_hba.conf
# change 'indent' to 'trust' in below line
host    all             all             127.0.0.1/32            trust
host    all             all             0.0.0.0/0            trust
```
# Edit postgresql.conf file
```code bash
# Add listen_addresses = '*' line in postgresql.conf file and save the file
sudo vim /var/lib/pgsql/9.6/data/postgresql.conf
```

# Restart PostgreSQL
```code bash
# Restart after edit pg_hba.conf file
sudo systemctl restart postgresql-9.6
```
# Create database and user role in PostgreSQL 9.6
```
sudo su - postgres
```
# To create DB user for JIRA
```
createuser --interactive -P jirauser
```
# Create database for JIRA
```
psql
CREATE DATABASE jiradb WITH ENCODING 'UNICODE' LC_COLLATE 'C' LC_CTYPE 'C' TEMPLATE template0;
GRANT ALL PRIVILEGES ON DATABASE jiradb to jirauser;
\z
# To exit
\q
```

# SQL

\l - Display database

\c - Connect to database

\dn - List schemas

\dt - List tables inside public schemas

\dt schema1. - List tables inside particular schemas. For eg: 'schema1'.



# To run a SQL script file within a specific schema in a PostgreSQL database

```
-- file.sql
SET search_path = schema_name;

-- Your SQL statements here
CREATE TABLE schema_name.table_name (...);

psql -U username -d database_name -f file.sql
```

# Clean file_wal
```
pg_archivecleanup -d /database/pgdata/12/archive 000000110000004D000000C2

pg_archivecleanup -d /database/pgdata/12/main/pg_wal 0000001100000033000000E3
```


# Grant Quyền select all other schema_name in database
```
postgres=# \l
                               List of databases
postgres=# \c database_name
You are now connected to database "innofinv2" as user "postgres".
innofinv2=# GRANT SELECT ON ALL TABLES IN SCHEMA scheame_name to user_name;
```
