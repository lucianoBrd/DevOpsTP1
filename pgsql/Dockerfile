#docker build -t lucianobrd/pgsql pgsql/
#docker run --rm --name pgsql -e POSTGRES_PASSWORD=123 -v /my/own/datadir:/var/lib/postgresql/data lucianobrd/pgsql
#docker run --link pgsql -p 8080:8080 adminer

FROM postgres:11.6-alpine

ENV POSTGRES_DB=db \
    POSTGRES_USER=usr \
    POSTGRES_PASSWORD=pwd

COPY 01CreateSchema.sql /docker-entrypoint-initdb.d
COPY 02InsertData.sql /docker-entrypoint-initdb.d
