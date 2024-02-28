# How to Kill a Process ID in PostgreSQL

Step 1: Find the Running Processes

```
SELECT * FROM pg_stat_activity;
SELECT datname, pid, usename, query FROM pg_stat_activity;
```

datename - It represents the name of databases.
pid - It indicates the process id.
Usename - usename is the name of the user in the PostgreSQL server.
Client_addr - client_addr specifies the client address which is shown as the client IP. Using this IP address, the client and server establish a connection.
Client_port - The client _port specifies the port numbers for all clients that are available on the server.
Xact_start - The xact_start means the start time transaction.
Backend_start - The backend _start column specifies the start time of the respective process when the client is connected.
Query_start - The query_start shows the time when the query begins/starts its execution.
State - This specifies the current status of the process/transaction that can be active or idle.
Query - This shows all executed queries.

Step 2: Find Non-Idle Processes/Queries
```
SELECT datname, pid, usename, query FROM pg_stat_activity WHERE STATE !='idle';
```

Step 3: Kill the Process ID
Stop
```
SELECT pg_cancel_backend(20280);
```
Kill
```
SELECT pg_terminate_backend(20280);
```

We run the “pg_cancel_backend(pid)” query before the “pg_terminate_backend(pid)” because the “pg_cancel_backend(pid)” query is safer than the “pg_terminate_backend(pid)”. The “pg_cancel_backend(pid)” tends to be lenient and takes more time to run.

Step 4: Find the Long-Running Queries
```
SELECT
  pid AS process_id,
  now() - pg_stat_activity.query_start AS query_duration,
  query, state
 FROM pg_stat_activity
 WHERE (now() - pg_stat_activity.query_start) > interval '10 minutes';
```

Refer: https://commandprompt.com/education/how-to-kill-a-process-id-in-postgresql/#:~:text=To%20kill%20a%20process%20in,to%20kill%20the%20selected%20processes.
