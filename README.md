# [MyDocker](https://training.play-with-docker.com/)
Clone github Repo
```
git clone https://github.com/dockersamples/linux_tweet_app
```
start a new container and tell it to run the hostname command. 

The container will start, execute the hostname command, then exit.
```
docker container run alpine hostname
```
Docker keeps a container running as long as the process it started inside the container is still running. 

In this case the `hostname` process exits as soon as the output is written. 

This means the container stops. However, Docker doesn’t delete resources by default, so the container still exists in the Exited state.

List all containers.
```
docker container ls --all
```
Containers which do one task and then exit can be very useful. 

You could build a Docker image that executes a script to configure something. 

Anyone can execute that task just by running the container - they don’t need the actual scripts or configuration information.

### Run a Docker container and access its shell.
```
docker container run --interactive --tty --rm ubuntu bash

--interactive says you want an interactive session.
--tty allocates a pseudo-tty.
--rm tells Docker to go ahead and remove the container when it’s done executing.
The first two parameters allow you to interact with the Docker container.
We’re also telling the container to run bash as its main process (PID 1).
When the container starts you’ll drop into the bash shell with the default prompt root@<container id>:/#. 
Docker has attached to the shell in the container, relaying input and output between your local session and the shell session in the container.
```
Run the following commands in the container.
```
ls /
ps aux
cat /etc/issue      --return the version of our host VM
exit to leave the shell session. This will terminate the bash process, causing the container to exit.
```
As we used the --rm flag when we started the container, Docker removed the container when it stopped. 

This means if you run another docker container ls --all you won’t see the Ubuntu container.

```
# Docker version
docker version

# List all docker images
docker image ls

# install ngnix 
docker image pull nginx

```
An image is a blue pring to a container.

```
docker container ls     // will give empty. Because images 
                        // are not container                      
```
Running a container
```
docker container run -d -p 80:80 --name mywebapp dkitaw/myfirstapp