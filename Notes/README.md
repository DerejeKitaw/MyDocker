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
## Run an interactive Ubuntu container
```
docker container run --interactive --tty --rm ubuntu bash
```
> * `--interactive` says you want an interactive session.
> * `--tty` allocates a pseudo-tty.
> * `--rm` tells Docker to go ahead and remove the container when it’s done executing. This means if you run another docker container ls --all you won’t see the Ubuntu container.

> * We’re also telling the container to run bash as its main process (PID 1).

> * When the container starts you’ll drop into the bash shell with the default prompt `root@<container id>:/#`.

* Run the following commands in the container.

```
> ls /
# will list the contents of the root director in the container.
```
```
> ps aux
# will show running processes in the container.
```
```
>cat /etc/issue
# will show which Linux distro the container is running, in this case Ubuntu 16.04.3 LTS.
```
```
>exit
# will terminate the bash process, causing the container to exit.
```
>Interactive containers are useful when you are putting together your own image. You can run a container and verify all the steps you need to deploy your app, and capture them in a Dockerfile.

> You can commit a container to make an image from it - but you should avoid that wherever possible. It’s much better to use a repeatable Dockerfile to build your image. 
