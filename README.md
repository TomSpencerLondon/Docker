# Docker for Java Developers

### List all Docker images
```bash
    docker images -a
```

### List all running docker containers
```bash
    docker ps
```

### Start a docker container
```bash
    docker start <container name>
```

### Stop a docker container
```bash
    docker stop <container name>
```

### kill all running containers
```bash
    docker kill ${docker ps -q}
```

### view logs of running docker container
```bash
    docker logs <container name>
```

### Delete all stopped docker containers
Use -f option to nuke the running containers also:
```bash
    docker rm ${docker ps -a -q}
```

### Remove docker image
```bash
    docker rmi <image name>
```

### Delete all docker images
```bash
    docker rmi ${docker images -q}
```

### Delete all untagged (dangling) docker images
```bash
    docker rmi ${docker images -q -f dangling=true}
```

### Delete all Images
```bash
    docker docker rmi ${docker images -q}
```

### Remove dangling volumes
```bash
    docker volume rm -f ${docker volume ls -f dangling=true -q}
```

### SSH Into Running Docker Container
Gives a bash shell in the container
```bash
    sudo docker exec -it <container name> bash
```

### view logs of running docker container
Run from directory of your docker-compose.yml file:
```bash
    docker-compose build .
```

### Use Docker Compose to Start a Group of Containers
Use this command from directory of docker-compose.yml file:
```bash
    docker-compose up -d
```
This will tell Docker to fetch the latest version of the container from the repo
and not use the local cache:

```bash
    docker-compose up -d --force-recreate
```

This can be problematic if you're doing CI builds with Jenkins and pushing
Docker images to another host, or using for CI testing. I was deploying a Spring
Boot Web Application from Jenkins, and found the docker container was not getting refreshed
with the lateste Spring Boot artifact.

```bash
# stop docker containers, and rebuild
docker-compose stop -t 1
docker-compose rm-f 
docker-compose pull
docker-compose build
docker-compose up -d
```

### Follow the logs of running docker containers with Docker Compose
```bash
docker-compose logs -f
```

### Save a running docker container as an image
```bash
docker commit <image name> <name for image>
```

### Follow the logs of one container running under Docker compose
```bash
docker-compose logs pump <name>
```

### Add Oracle Java to an Image
For CentOS/ RHEL

```bash
ENV JAVA_VERSION 8u31
ENV BUILD_VERSION b13

# Upgrading system
RUN yum -y upgrade
RUN yum -y install wget
# Downloading & Config Java 8
RUN wget --no-cookies --no-check-certificate --header "Cookie:
oraclelicense=accept-securebackup-cookie"
"http://download.oracle.com/otn-pub/java/jdk
/$JAVA_VERSION-$BUILD_VERSION/jdk-$JAVA_VERSION-linuxx64.
rpm" -O /tmp/jdk-8-linux-x64.rpm
RUN yum -y install /tmp/jdk-8-linux-x64.rpm
RUN alternatives --install /usr/bin/java jar /usr/java/latest/bin/java
200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest
/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac
200000
PAGE
```

### Add / Run a Spring Boot Executable Jar to a Docker Image
```bash

ADD /maven/myapp-0.0.1-SNAPSHOT.jar myapp.jar
RUN sh -c 'touch /myapp.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","
/myapp.jar"]
```
### Show Running Containers
```bash
docker ps
```

### Show All Containers - Running and stopped
```bash
docker ps -a
```

### Default Tag
'latest' is selected if no other value is specified

### Run A Docker Image
```bash
docker run <image name>
```

### See the Console Output of a Docker Container
```bash
docker logs <container name>
```

### Build a docker image
From the directory of the Dockerfile run:
```bash
docker build -t <tag name>
```

### Stop a docker container
```bash
docker kill <container name>
# or
docker stop <container name>
```


### Parameter that tells docker to run the container as a background process
```bash
-d
```

### Example: docker run -d <image name>
List all docker images on your system
```bash
docker images
```


### Map a Host Port to a Container Port
```bash
-p <host port>: <container port>
```
Example:
```bash
docker run -p 8080:8080 <image name>
```

### Tail the Console Output of a Running Docker Container
```bash
docker logs -f <container name>
```

### A .java file to a docker image - i.e. the source code
The Dockerfile

### Remove a Stopped Docker Container
```bash
docker rm <container name>
```
### Specify an Environment Variable for a Docker Container
```bash
docker run -e MY_VAR=my_prop <image name>
```

### Remove a Docker Image from your System
```bash

docker rmi <image name>
```

#### Shell into a Running Docker Container
```bash
docker exec -it <container name> bash
```


### Share Storage on a Host System with a Docker container
```bash
-v <host path>: <container path>
```
Example:
```bash
docker run -v <host path>: <the container path> <image name>
```

### Name of the Maven plugin we are using for the Course
Fabric8


### Map a Host Port to a Container Port
```bash
-p <host port>:<container port>
```
Example:
```bash
docker run -p 8080:8080 <image name>
```

### Maven Command to Stop Running Image(s)
```bash
mvn docker:stop
```

### Maven Command to Build a Docker Image
```bash
mvn clean package
docker:build
```

### Remove a Stopped Docker Container
```bash
docker rm <container name>
```

### Maven Command Used to Publish a Docker Image to its Repository
```bash
mvn docker:push
```

### Maven Command Used To Start a Docker Image
```bash
mvn docker:start
```

### Run Containers in the Background from Maven
```bash
mvn docker:start
```

### XML Tag that has the Runtime Parameters for the Fabric8 Plugin
```xml

<image>
    <run>
        **params here**
    </run>
</image>

```

### Map a Host Port to a Container Port in Maven Configuration
```bash
<ports>
<port>8080:8080</port>
</ports>
```

### Parameter that Creates a Network Host Name Reference for a Docker Container to Another Container
```bash

"--link" {dash dash}
--link <container name>:<hostname>
```

### Specify Environment Variable for a Docker Container in Maven
```bash
Configuration
<env>
<parameter_name>{value}</parameter_name>
</env>

```
### Maven Command Used To Start a Docker Image Interactively
```bash
mvn docker:run
```

### Where to Store Credentials
~/.m2/settings.xml

Example:

```xml
<servers>
    <server>
        <id>docker.io</id>
        <username>springframeworkguru</username>
        <password>YourPasswordHere</password>
    </server>
    
</servers>

```

### Docker for Java Developers

### What is Docker?
- Docker is a standard for Linux containers
- A "Container" is an isolated runtime inside of Linux
- A "Container" provides a private machine like space under Linux
- Containers will run under any modern Linux Kernel

### Containers can:
- Have their own process space
- Their own network interface
- Run processes as root (inside the container)
- Have their own disk space
  - They can share with the host too

<img width="539" alt="image" src="https://user-images.githubusercontent.com/27693622/224767443-94cc271a-a9c4-4a5f-afab-226623e0ae0e.png">


### Docker Terminology
- Docker Image - The representation of a Docker Container. Kind of like a JAR or WAR file in Java
- Docker Container - The standard runtime of Docker. Effectively a deployed a running Docker image. Like a Spring
Boot executable
- Docker Engine - The code which manages Docker stuff. Creates and runs Docker Containers

<img width="291" alt="image" src="https://user-images.githubusercontent.com/27693622/224768279-fe31b4f6-ef5d-46e2-a6ee-2eaf0fe8697c.png">

### Docker - hello world
```bash
docker run hello-world
```

### Dockerhub
https://hub.docker.com

#### Mysql image
https://hub.docker.com/_/mysql
```bash
docker pull mysql
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
```
https://hub.docker.com/_/postgres
```bash
docker pull postgres
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```
