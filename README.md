# [MyDocker](https://training.play-with-docker.com/)
[official Doc](https://youtu.be/V9IJj4MzZBc)

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
### Run a background MySQL container
```
docker container run \
 --detach \
 --name mydb \
 -e MYSQL_ROOT_PASSWORD=my-secret-pw \
 mysql:latest
```
```
--detach will run the container in the background.
--name will name it mydb.
-e will use an environment variable to specify the root password (NOTE: This should never be done in production).
```
```
docker container ls
```
You can check what’s happening in your containers by using a couple of built-in Docker commands: 
```
docker container logs and 
docker container top.
```
### Example
```
# To see logs from the MySQL Docker container.
docker container logs mydb
# To see the process running inside the container.
docker container top mydb
```
Although MySQL is running, it is isolated within the container because no network ports have been published to the host. Network traffic cannot reach containers from the host unless ports are explicitly published.

### docker container `exec` allows you to run a command inside a container. 
```
docker exec -it mydb \
 mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version

 # equivalent of mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version inside our MySQL container.
 ```
### docker container `exec` to connect to a `new shell process` inside an already-running container. Executing the command below will give you an interactive shell (sh) inside your MySQL container.
```
docker exec -it mydb sh

# Notice that your shell prompt has changed. This is because your shell is now connected to the sh process running inside of your container.

mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
will return the same output is the same as before.

Type `exit` to leave the interactive shell session.
```



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
