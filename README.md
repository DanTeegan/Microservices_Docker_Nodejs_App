# Microservices_Docker_Nodejs_App

### What is Docker?
- It is an open source platform for containerisation
- Docker enables you to separate your infrascture so you can deliver your software quickly
- It is written in the language Go

### Why should we use Docker?
- Because it doesn’t make a difference what OS you are using
- Makes our life a lot easier only 1 line command to spin up nginx and port mapping
- Docker is fast
- Provides consistent delivery of your applications.
In our class we had people using different OS. We all created containers and images and we where all able to smoothly use each other containers. We could pull from docker hub retag it and push to our own dockerhub.

### What is container?
- Process of spinning up virtual environments within containers.
- You can pull any container, change the container re tag it and make changes. You can then repush that new container

### Benefits of containers
- Creating a vm to test out all operating systems, test installation of software

### What is the difference between VMs and Docker
- Docker is lightweight compared to VMs… but how? Docker shares the resources of an OS then creating a entire virtual environment.

### Microservices

Microservices – Also known as the microservice architecture is an architecture style that structures an application as a collection of services that are:
Highly maintainable and testable
- loosely coupled
- Independently deployable
- Organized around business capability’s
- Owned by a small team


### Microservices Docker Nodejs App and db task

App Docker file

```
# select base image to build our own customised node app microservice

FROM node:alpine

# working directory inside the container

WORKDIR /usr/src/app

# copy dependencies

COPY package*.json ./

# Install npm

RUN npm install

# copy everything from current location to default location inside the container

COPY . .

# define the port

EXPOSE 3000

# start the app with CMD

CMD ["node","app.js"]

```


docker-compose file

```
version: '3'

services:
  db:
    image: mongo
    restart: always
    ports: [27017:27017]

  web:
    build: ./app
    restart: always
    ports: [3000:3000]
    environment:
      - DB_HOST=mongodb://db:27017/posts
    depends_on:
      - db


```

