## postgres 10 with docker on ubuntu

Adapted from [here](https://hackernoon.com/dont-install-postgres-docker-pull-postgres-bee20e200198)

Assume there is local postgres running (which is 9.5 in ubuntu 16.04) and we want to have also Postgres 10 installed.
The new postgres will run on port 5433

* Pull postgres 10

```bash
docker pull postgres:10
```


* Create local volumes (so it would be persistent)
```bash
mkdir -p $HOME/docker/volumes/postgres
```

* Run 
```bash
docker run --rm   --name pg-docker -e POSTGRES_PASSWORD=docker -d -p 5433:5432 -v $HOME/docker/volumes/postgres:/var/lib/postgresql/data  postgres:10
```

* Connect
```bash
psql -h localhost -U postgres -d postgres -p 5433
```

* Edit ~/.pgpass file, to avoid entering password
```bash
echo "localhost:5433:*:postgres:docker" >> ~/.pgpass
```

* opentrain restore
```bash
python manage.py sqlcreate -D | psql -h localhost -U postgres -d postgres -p 5433
gunzip -c ~/Downloads/db_2019_03_30_14_29_46.sql.gz | m dbshell
```
