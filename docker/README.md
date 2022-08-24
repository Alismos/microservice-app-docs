# Create docker images and runing services

## Frontend Dockerfile

![image](assets/images/fronte_docker.png)

### build Dockerfile

$ sudo docker build -t <docerkhub_name>/<image_name>:<version> -t daramirezs/users-api:latest . 

## Users Dockerfile

![image](assets/images/users_docker.png)

### build docker 

$ sudo docker build -t daramirezs/users-api:1.0 -t daramirezs/users-api:latest . 

## Auth Dockerfile

![image](assets/images/auth_docker.png)

$ sudo docker build -t daramirezs/auth-api:1.0 -t daramirezs/auth-api:latest . 

## Todos Dockerfile

![image](assets/images/todos_docker.png)

$ sudo docker build -t daramirezs/todos-api:1.0 -t daramirezs/todos-api:latest . 

## Deploy service in ec2 instance

Requiremtents: 

* [Install docker](https://docs.docker.com/engine/install/ubuntu/)

Pull image from dockerhub

$ docker pull |user|/|image|:

Run docker

$ sudo docker run -e PORT="8080" -e AUTH_API_ADDRESS=" <service_domain>:<port> " -e TODOS_API_ADDRESS="http://<service_domain>:<port>" -e ZIPKIN_URL=" <service_domain>:<port> " --name frontend -p 8040:8040 -d daramirezs/frontend:1.0 

Checking frontend service:

![image](assets/images/frontend_service.png)

## Redis service with docker-compose

![image](assets/images/todos_docker-compose.png)

Logging redis-server

![image](assets/images/redis_server.png)

Logging todos-api

![image](assets/images/todos-api.png)

Logging log-processor

![image](assets/images/log-processor.png)

Application

![image](assets/images/application.png)

Zipkin-server

![image](assets/images/zipkin.png)