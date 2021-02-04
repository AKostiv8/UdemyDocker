# UdemyDocker
 Docker course

## Build Docker image steps

`docker login` - to authenticate

`docker build -t <dockerhub name>/<image name> .`
`docker build -t anastasiia/docker-r-studio .` 

## List images
`docker images`

## Run the container
`docker run`

`docker run --rm -p 8787:8787 anastasiia/docker-r-studio`

`docker run --rm -p 8787:8787 -e USER=myself -e PASSWORD=guest anastasiia/docker-r-studio`

## Mapping folders
--using option -v to map computer and container file system

`docker run --rm -p 8787:8787 -e USER=myself -e PASSWORD=guest -v /Users/anastasiia_kostiv/Documents/Udemy_Course_Shared:/home/myself/r-studio anastasiia/docker-r-studio`