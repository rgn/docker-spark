# docker-spark

This repo provides a single node Spark contaienr with a postgres metastore backend including Delta.io.

spark: 3.5.0
delta.io: 3.3.0

## Running locally

A `docker-compose` environment starts a Spark Thrift server and a Postgres database as a Hive Metastore backend.

The following command starts two docker containers:

```sh
docker-compose up -d
```

It will take a bit of time for the instance to start, you can check the logs of the two containers.
If the instance doesn't start correctly, try the complete reset command listed below and then try start again.

Connecting to the local spark instance:

* The Spark UI should be available at [http://localhost:4040/sqlserver/](http://localhost:4040/sqlserver/)
* The endpoint for SQL-based testing is at `http://localhost:10000` and can be referenced with the Hive or Spark JDBC drivers using connection string `jdbc:hive2://localhost:10000` and default credentials `hive`:`hive`

Note that the Hive metastore data is persisted under `./.hive-metastore/`, and the Spark-produced data under `./.spark-warehouse/`. To completely reset you environment run the following:

```sh
docker-compose down
rm -rf ./.hive-metastore/
rm -rf ./.spark-warehouse/
```