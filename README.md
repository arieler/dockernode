docker build -t dockernode .

docker run -dp 3000:3000 dockernode

http://localhost:3000/

Remove a running container

docker ps

# Swap out <the-container-id> with the ID from docker ps
docker stop <the-container-id>

# Once the container has stopped, you can remove it
docker rm <the-container-id>

# Working with named volumes
docker volume create todo-db

docker run -dp 3000:3000 -v todo-db:/etc/todos dockernode

# inspect where docker is storing the volume
docker volume inspect todo-db

# Powershell (binded volumes)
docker run -dp 3000:3000 `
     -w /app -v "$(pwd):/app" `
     node:12-alpine `
     sh -c "yarn install && yarn run dev"

docker logs -f <container-id>


# Working with mysql

# 1 create a network

docker network create todo-app

docker run -d `
     --network todo-app --network-alias mysql `
     -v todo-mysql-data:/var/lib/mysql `
     -e MYSQL_ROOT_PASSWORD=secret `
     -e MYSQL_DATABASE=todos `
     mysql:5.7

# enter to the mysql container

docker exec -it <mysql-container-id> mysql -p

# Docker Compose

 docker-compose up -d

 docker-compose down