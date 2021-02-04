# UdemyDocker
 Docker course

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
