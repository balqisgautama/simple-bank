# Simple Bank
The service that we’re going to build is a simple bank.
It will provide APIs for the frontend to do following things:
- First, create and manage bank accounts, which are composed of owner’s name, balance, and currency.
- Second, record all balance changes to each of the account. So every time some money is added to or subtracted from the account, An account entry record will be created.
- And third, perform a money transfer between 2 accounts. This should happen within a transaction, so that either both accounts’ balance are updated successfully or none of them are.

## ERD
https://dbdiagram.io/d/647fecc3722eb774948590ca

## Installation
Simple bank require Go 1.20+ , Docker v4.18+ , PostgreSQL 12.0+

## PostgreSQL Docker Container
source : https://hub.docker.com/
```sh
docker pull <image>:<tag>
docker pull postgres:12-alpine
```
```sh
docker images
```
```sh
docker run --name <container_name> -e <environment_variable> -p <host_ports:container_ports> -d <image>:<tag>
docker run --name postgres12 -p 5432:5432 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=secret -d postgres:12-alpine
```
```sh
docker ps
```
```sh
  docker exec -it postgres12 createdb --username=root --owner=root udemy
```
```sh
docker exec -it <container_name_or_id> <command> [args]
docker exec -it postgres12 psql -U root
```
```sh
select now();
\q
CREATE SCHEMA IF NOT EXISTS "simple_bank";
```
```sh
docker logs <container_name_or_id>
docker logs postgres12
```

## PostgreSQL Migrate Golang
source : 
- https://github.com/golang-migrate/migrate
- https://scoop.sh/

```sh
scoop install migarte
scoop -v
```
```sh
migrate create -ext sql -dir db/migration -seq init_schema
```
```sh
migrate -path db/migration -database "postgresql://root:secret@localhost:5432/udemy?search_path=simple_bank&sslmode=disable" -verbose up
```
