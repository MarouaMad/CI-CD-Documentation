---
sidebar_position: 1
---

# Docker Tutorial
## Introduction
* Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.

## Dockerfile

* Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.

### Dockerfile for nodejs application 
```
FROM node:20.5.1-alpine3.18    <!-- A Dockerfile must begin with a FROM instruction.The FROM instruction specifies the Parent Image from which you are building. -->
WORKDIR /app             <!-- create a folder -->
COPY package*.json  .   <!-- copy application dependencies -->
RUN npm install          <!-- install dependencies -->
COPY . .                      <!-- copy app code -->
EXPOSE 3000                    <!-- open port number 3000 -->
CMD ["npm","start"]              <!-- run the app -->
```


### Dockerfile for nodejs application with optimzed image & multistage 

```

FROM node:20.5.1 as build                    <!-- build is the name of the stage -->
WORKDIR /app
COPY package*.json  .
RUN npm install
COPY . .
RUN npm run build                             <!-- build the artifact -->

FROM nginx:stable-alpine as prod              <!-- nginx is a used as a server web to run app   -->
WORKDIR /user/share/nginx/html
COPY --from=build /app/build .

```

# Commad to build an image from   Dockerfile 
```
docker build -t mynewimage  .
```

## Docker commands

List of runinng container 

```
docker ps    
```

List of containers running and stopped containers 

```
docker ps -a 
```
stop a running container by id or by container name 
```
docker stop my_container
```
start a container by mentionning the name or the ID 
 ```
 docker start  my_container 
 ```
 download an image from the dockerhub repository 
 ```
 docker pull imageName 
 ```
pull the image and start the container 

```
docker run -d --name mycontainer  -p 80:80  
```


