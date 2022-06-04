# USING CONTAINERS

# basic
docker --version

# login
docker login

# pull image
docker pull nginex

# look at currently available images
docker images

# run instance of an image
docker run nginx:latest - docker run <image>:<tag>

-d - detached mode
docker -d run nginx:latest

-p 8080:80 - map port 80 in container to 8080 in localhost
docker run -p 8080:80 -p 3000:80 nginx:latest

--name <name>
docker --name website nginx:latest

## sharing files between host and container
 -v C:\Users\szulc\Documents\Code\docker\volume:/usr/share/nginx/html:ro - it maps folder "volume" in host to folder "html" in container, "ro" - read only, without "ro" the folder will be editable also inside container

## sharing files between container and containers
 --volumes-from <container_name> - mount folder that is already mounted to another container


# stop container
docker stop <container_id>/<name>

# start container
docker start <id>/<name> - you can only start already created containers, not images

# list of working containers
docker container ls
docker ps - it lists only running containers
- a - show all containers
- q - show only IDs

--format - to format output of a command
docker ps --format="ID\t{{.ID}}\nNAME\t{{.Names}}\n"
.ID
.Names
.Image
.Ports
.Command
.CreatedAt
.Status

# remove container
docker rm <id>/<name>
docker rm $(docker ps -aq) - remove all containers

-f - to force to remove even currently running container

# remove images
docker rmi <id>

# execute commands in container
docker exec <name>/<id> <command>

docker exec -it website bash - enter interactive mode


# BUILDING CONTAINERS
The build is created in Dockerfile

FROM node:latest
WORKDIR /app
ADD . .
RUN npm install
CMD node index.js

docker build -t <name>:<version> . - create image from Dockerfile 

FROM - select base of a container
WORKDIR /app - from this point every command will be executed in this folder
ADD <host> <container> - copy files from host to container
RUN <command> - it will be run and commited to the container (it changes state of the container), there may be many run commands, they are ment to build
CMD <command> - the command is executed just once, to run the whole applciation at the end

RUN vs CMD
https://stackoverflow.com/questions/37461868/difference-between-run-and-cmd-in-a-dockerfile

## Ignoring files
We don't want to copy dependencies, we want to download them when we create an image. The ignore list is inside .dockerignore

## Using cache
We don't want to download the same dependencies when we do minor change in a source code.

Example from video
We should change

FROM node:latest
WORKDIR /app
ADD . .
RUN npm install
CMD node index.js

to

FROM node:latest
WORKDIR /app
ADD package\*.json . <- \* means just star (error in .md)
RUN npm install
ADD . .
CMD node index.js

Becuase then when it firstly adds both package files and see there is no change it will use cash for that step and then every run would look the same because the current files are the same. 

## Reduce size of images - Alpine
Instead of using node:latest we can use node:lts-alpine image which is considerably smaller 1GB -> 100MB.

## tagging

docker tag albert-website:latest albert-website:1 <- it creates different image with different tag

## inspecting
docker inspect <container_name>/<id>

## logs
docker logs <container_name>/<id>

-f - to "follow"/listen to appearing new logs


# KNOWLEDGE
- Container is a running instance of an image
- containers sometimes appear to work in browser because the result of 


# HOW TO RUN REACT
To run react with docker using node image add:
RUN apk --no-cache add --virtual .builds-deps build-base python3

FROM node:16.14-alpine
RUN apk --no-cache add --virtual .builds-deps build-base python3
WORKDIR /app
ADD package\*.json .
RUN npm install
ADD . .
CMD npm start

# Get rid of vmmem process

wsl --shutdown