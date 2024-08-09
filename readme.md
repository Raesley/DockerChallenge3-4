//Build image:

docker build -t node-api:v1

//Create network: 

docker network create node-api-network

(Node and MySQL need to communicate without exposing ports publicly.)

//Start MYSQL:

docker run 

--rm
-d
--name mysql_server
-e MYSQL_DATABASE='database'
-e MYSQL_USER='username'
-e MYSQYL_PASSWORD='password'
-e MYSQL_ROOT_PASSWORD='root'
--network node-api-network
mysql:8.0

//Start node-api

docker run
--rm
--name node-app
--network node-api-network
-p 8080:8080
-v $(pwd):/app
node-api:v1

//Stop container

docker stop node-app
docker stop mysql_server

// Start

docker-compose up

//optionally stop

docker-compose down