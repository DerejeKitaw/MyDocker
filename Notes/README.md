# [Task 1:](https://training.play-with-docker.com/beginner-linux/#Task_1) 
> Run some simple Docker containers
## Run a single task in an Alpine Linux container
```
docker container run alpine hostname
```
* The container will start, execute the hostname command, then `exit`.
* If `alpine:latest` image could not be found locally, Docker automatically pulls it from Docker Hub.
* Docker keeps a container running as long as the process it started inside the container is still running.
>In this case the hostname process exits as soon as the output is written. This means the container stops. However, Docker doesn’t delete resources by default, so the container still exists in the Exited state.
## List all containers
```
docker container ls --all
```
* Notice `Alpine Linux container` is in the `Exited` state.
* The container ID is the hostname that the container displayed.
> * Containers which do one task and then exit can be very useful. 
> * You could build a Docker image that executes a script to configure something. 
> * Anyone can execute that task just by running the container - they don’t need the actual scripts or configuration information.
