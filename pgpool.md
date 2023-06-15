# Monitoring PostgreSQL Cluster via Pgpool-II with Prometheus

Building and running Pgpool-II Exporter

```
docker run --name pgpool2_exporter \
  --net=host --rm \
  -e POSTGRES_USERNAME=<username> \
  -e POSTGRES_PASSWORD=<password> \
  -e POSTGRES_DATABASE=<database> \
  -e PGPOOL_SERVICE=<hostname> \
  -e PGPOOL_SERVICE_PORT=<port> \
  -e SSLMODE=<sslmode> \
  pgpool/pgpool2_exporter:latest
```

The following environment variables configure the docker container:

* POSTGRES_USERNAME PostgreSQL user name. Default is postgres.

* POSTGRES_PASSWORD PostgreSQL user password. Default is postgres.

* POSTGRES_DATABASE Database name. Default is postgres.

* PGPOOL_SERVICE Pgpool-II hostname. Default is localhost.

* PGPOOL_SERVICE_PORT Pgpool-II port number. Default is 9999.

* SSLMODE Whether or not to use SSL. Default is disable. Valid values: disable, require, verify-ca, verify-full.
 
 ```
 docker run -d --name pgpool2_exporter \
  --net=host --rm \
  -e POSTGRES_USERNAME=postgres \
  -e POSTGRES_PASSWORD=xxx \
  -e POSTGRES_DATABASE=ucm_sme \
  -e PGPOOL_SERVICE=xxx \
  -e PGPOOL_SERVICE_PORT=9999 \
  -e SSLMODE=disable \
  pgpool/pgpool2_exporter:latest
 ```
 
Metrics
 
Once Pgpool-II Exporter is running, you can verify the metrics that are being exported using curl command.

$ curl -s localhost:9719/metrics

After creating a Prometheus data source to Grafana you can add the following graphs
![image](https://github.com/anhln12/postgresql/assets/18412583/0a294207-cac8-494c-aacf-1d380472aad5)

[refer](https://github.com/pgpool/pgpool2_exporter)
