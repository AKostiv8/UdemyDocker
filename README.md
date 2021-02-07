# UdemyDocker
 Docker course

![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/nolik2000/docker-r-studio)

## Build Docker image steps

`docker login` - to authenticate

`docker build -t <dockerhub name>/<image name> .`
`docker build -t nolik2000/docker-r-studio .` 

## List images
`docker images`

## Run the container
`docker run`

`docker run --rm -p 8787:8787 nolik2000/docker-r-studio`

`docker run --rm -p 8787:8787 -e USER=myself -e PASSWORD=guest nolik2000/docker-r-studio`

## Mapping folders
--using option -v to map computer and container file system

`docker run --rm -p 8787:8787 -e USER=myself -e PASSWORD=guest -v /Users/anastasiia_kostiv/Documents/Udemy_Course_Shared:/home/myself/r-studio nolik2000/docker-r-studio`

## Create executable file
-- using vim editor to create and edit file

--command `chmod +x filename` to make file executable

`vim Run_RStudio` - creating executable file (to start writing press `i`), to save file press `esc`, then `:wq` (w - write, q - quite)

`chmod +x Run_RStudio` - make file executable

## Save image to Docker Hub
`docker login`

`docker push nolik2000/docker-r-studio`

## Saving image locally in .tar file/archive

`docker save nolik2000/docker-r-studio > docker-r-studio.tar`

## Removing images
`docker images`

`docker rmi 03703b737ba3` - remove by IMAGE ID OR By name


## Restore the image from local archive
`docker load --input [name of the archive file]`

`docker load --input docker-r-studio.tar`


## Check running container from another terminal
`docker container ls` OR `docker ps`

Execute bash script in container:
`docker ps`

`docker exec -it [CONTAINER ID] bash`

## Install package in R Studio
! We need to save the state of that image while container is running, so go to terminal:

`docker ps`

`docker commit -m "added package name" [CONTAINER ID] [IMAGE NAME]`

`docker commit -m "added package name" 6130ce9edade nolik2000/docker-r-studio` - now image updated


## Push changes to Docker Hub
`docker push <dockerhubuser>/<imagename>`

`docker push nolik2000/docker-r-studio` 

## Save new version of the image using tags

`docker tag nolik2000/docker-r-studio nolik2000/docker-r-studio:Version0.9`

`docker images`

`docker push nolik2000/nolik2000/docker-r-studio:Version0.9`


## Setup Automated Build of the image
--we can link both Docker Hub and GitHub accounts

--change in the code will rebuild the image. Automatically!

## Verify Automated build
--the image locally is not obviously the same is not in Docker Hub, Dockerhub has a newer image because it was built on the Docker Hub Servers, so good to do `pull` in this case

`docker pull nolik2000/docker-r-studio`

### ========================================================

## Build Another Docker image

--We have built docker image directly on Dockerhub via connection GitHub with DockerFile

-- It is usually recommended when we already sure that build will work

## Pull out image locally to your computer
 `docker pull nolik2000/docker-r-h2o`

##Test container

`docker images`

`run exec file` - inside you can use R bash commands like sd(5), search() etc

## Verify stopped containers

`docker ps -a`


### =============================================

`Dockerfile` contains sets of instructions to build an image

Command `docker build .` will build the image on the local computer

Once the image is built we can launch the container with a command `docker run ...`

If necessary we can update the image from running container by executing a command `docker commit ...` (from another terminal)

Image can be stored (published) on the Docker Hub `docker push repoID/imageID`

Image can be saved locally `docker save imageID > imageID.tar`

Other users could get the image from Docker Hub with a command `docker pull repoID/imageID`

... or restore it from the archive with `docker load --input imageID.tar`

## Deleting un-used containers/images

Sometimes we can forget to launch our containers by specifying --rm key or there may be intermediate images with a failed build. Those objects may take some space (e.g. 10 GB) so it is a good practice to delete those. The easiest way to delete those is to execute command:

`docker system prune`


##Note on Docker Compose
Typically, in order to run multi-container applications, a dedicated method exists. This is called `docker-compose`. As this method per se is quite complicated to grasp it will not be covered in this section. Instead, a separate section on docker compose will be published to wrap up the course.

The idea will be to develop a fully functional multi-container application like this:

-Shiny App

-Plumber API

-Database

-Network

These will be assembled and started with one docker compose file.

Stay tuned, keep learning and don't forget to have some fun with this course!

## Establish network
`docker network create -d bridge my-net`

## List of available network
`docker network ls`

## Stop 2 containers

`docker container stop Dev API`

## Remove network

`docker network rm my-net`

## Inspect network

`docker network inspect my-net`
