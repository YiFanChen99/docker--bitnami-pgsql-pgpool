# docker--bitnami-postgresql-pgpool

Based on [bitnami/bitnami-docker-pgpool](https://github.com/bitnami/bitnami-docker-pgpool)

## Dispatch

```
docker-compose up -d
```

## Test connecting after run (by psql)

#### For pg-x node
```
psql -h localhost -p $HOST_PORT -d customdatabase -U $USERNAME
> Password for user $USERNAME: $PASSWORD
```
Get $HOST_PORT from container info. Or it can be defined on docker-compose.yml
$USERNAME/$PASSWORD can be either postgres/adminpassword or customuser/custompassword

#### For pgpool
```
psql -h localhost -p 5433 -d customdatabase -U postgres
> Password for user postgres: adminpassword
```
Unable to auth by user customuser

## Information

* Using bitnami/postgresql-repmgr:11 and bitnami/pgpool:4
* pg-x nodes must export port for repmgr/pgpool

## Custom config file

* For image `bitnami/postgresql-repmgr`, mount empty conf-dir into `/bitnami/repmgr/conf/` and restart.
* For image `bitnami/pgpool`, mount empty dir into somewhere. Copy pgpool-confs from `/opt/bitnami/pgpool/conf/` into mounted dir. Mount the dir into `/opt/bitnami/pgpool/conf/` and restart.

## Logs

* For `postgresql-repmgr`, mount log file at `/opt/bitnami/postgresql/logs/postgresql.log`.

## Jieba

Should manually do `CREATE EXTENSION pg_jieba;` after DB inited.
