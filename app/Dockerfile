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
