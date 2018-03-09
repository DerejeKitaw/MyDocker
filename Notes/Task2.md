# Task 2: 
## Package and run a `custom` app using Docker
```
git clone https://github.com/dockersamples/linux_tweet_app
cd ~/linux_tweet_app
cat Dockerfile
```
```
FROM nginx:latest

COPY index.html /usr/share/nginx/html
COPY linux.png /usr/share/nginx/html

EXPOSE 80 443     

CMD ["nginx", "-g", "daemon off;"]
```
> * `FROM` specifies the base image to use as the starting point for this new image you’re creating. For this example we’re starting from nginx:latest.
> * `COPY` copies files from the `Docker` host into the image, at a known location. In this example, COPY is used to copy two files into the image: index.html. and a graphic that will be used on our webpage.
> * `EXPOSE` documents which ports the application uses.
> * `CMD` specifies what command to run when a container is started from the image. Notice that we can specify the command, as well as run-time arguments.
## create a new Docker image using the instructions in the Dockerfile
```
docker image build --tag $DOCKERID/linux_tweet_app:1.0 .
```
> * --tag allows us to give the image a custom name. In this case it’s comprised of our DockerID, the application name, and a version. Having the Docker ID attached to the name will allow us to store it on Docker Hub in a later step
> * `.` tells Docker to use the current directory as the build context
> * Be sure to include period (`.`) at the end of the command.

## start a new container from the image created.
```
 docker container run \
 --detach \
 --publish 80:80 \
 --name linux_tweet_app \
 $DOCKERID/linux_tweet_app:1.0
```
> * As this container will be running an NGINX web server, we’ll use the --publish flag to publish port 80 inside the container onto port 80 on the host. This will allow traffic coming in to the Docker host on port 80 to be directed to port 80 in the container. The format of the --publish flag is `host_port`:`container_port`.
> * Any external traffic coming into the server on port 80 will now be directed into the container on port 80.

> * In a later step you will see how to map traffic from two different ports - this is necessary when two containers use the same port to communicate since you can only expose the port once on the host.

