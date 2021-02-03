# TP1 Docker

## Database

1 -  Build the db dockerfile
```$ docker build -t lucianobrd/pgsql pgsql/```
Here you build the Dockerfile of current folder (pgsql) and you call it as you want (nameDockerHub/pgsql)

2 -  Run the previously mounted image
```$ docker run --rm --name pgsql -e POSTGRES_PASSWORD=123 -v /my/own/datadir:/var/lib/postgresql/data lucianobrd/pgsql```
Don't need to put the port, we dont want to open it to everyone (5432 is postgres's default).
Then you give the container a name (here pgsql, cause it's just that).
-v Option means that you link your system's folder to the container datas to save them.
And you tell it to use your image (lucianobrd/pgsql).

3 - Now you have an up and running postgres container you need to verify it. Lets run an adminer.
```$ docker run --link pgsql -p 8080:8080 adminer```
So you create an adminer container, linked to the postgres (its the name) container you just mounted. You also give it 8080 port for both sides.

## Backend API

We need multistage build in order to build and run the app.

1 - Build the api dockerfile
```$ docker build -t lucianobrd/java java/simple-api```

2 - Run the container
```$ docker run -it --rm --link pgsql --name java lucianobrd/java```
Here you run the container and link it to the pgsql container in order to let your api ask your container

3 - To test the api from a browser, add option to last command ```-p 8080:8080```. Find the port if you dont know : ```docker port java```
http://localhost:8080/departments/IRC/students

[{"id":1,"firstname":"Eli","lastname":"Copter","department":{"id":1,"name":"IRC"}}]

## HTTP Server

We need a proxy for security.

1 - Build the image
```$ docker build -t lucianobrd/httpd httpd/```

2 - Run the container linking the api container on port 80
```$ docker run -dit --rm --link java --name httpd -p 80:80 lucianobrd/httpd```

3 - Test the server : http://loclhost

## Docker compose

Docker compose is very important, it allow to build, run, etc, all images.
```$ docker-compose up```
```$ docker-compose down```

## Publish

To publish images on docker hub :
```$ docker login```
```$ docker tag java lucianobrd/backend:latest```
```$ docker push lucianobrd/backend```


# Docker images :

* https://hub.docker.com/repository/docker/lucianobrd/devops_database
* https://hub.docker.com/repository/docker/lucianobrd/devops_backend
* https://hub.docker.com/repository/docker/lucianobrd/devops_httpd

# GitHub : 
* https://github.com/lucianoBrd/DevOpsTP1