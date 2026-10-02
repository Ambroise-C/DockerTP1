FROM postgres:17.2-alpine

ENV POSTGRES_DB=db \
   POSTGRES_USER=usr \
   POSTGRES_PASSWORD=pwd

COPY ./CreateScheme.sql /docker-entrypoint-initdb.d/CreateScheme.sql
COPY ./InsertData.sql /docker-entrypoint-initdb.d/InsertData.sql