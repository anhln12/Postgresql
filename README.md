# postgresql


Create database and user role in PostgreSQL 9.6
sudo su - postgres

To create DB user for JIRA
createuser --interactive -P jirauser

Create database for JIRA
```
psql
CREATE DATABASE jiradb WITH ENCODING 'UNICODE' LC_COLLATE 'C' LC_CTYPE 'C' TEMPLATE template0;
GRANT ALL PRIVILEGES ON DATABASE jiradb to jirauser;
\z
# To exit
\q
```
