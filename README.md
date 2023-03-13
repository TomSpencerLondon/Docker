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

https://hub.docker.com/r/nginxdemos/hello/
Run nginx to show in browser on port 8085 locally:
```bash
docker run -p 8085:80 -d nginx
```

https://hub.docker.com/_/mongo
Run mongo database:
```bash
docker run --name some-mongo -d mongo:tag
```
Run mongo database with exposed local port:
```bash
docker run -d  --name mongo-on-docker  -p 27888:27017 -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
```
- docker run runs the image and starts the container
- -d runs the container in background, so that we are free to use the current terminal instance
- --name mongo-on-docker defines a friendly name for the container
- -p 27888:27017 declares that the local port 27888 is mapped to the internal 27017 port
- -e MONGO_INITDB_ROOT_USERNAME=mongoadmin sets the root username (-e sets the environment variables)
- -r MONGO_INITDB_ROOT_PASSWORD=secret sets the root password;
- mongo is the name of the image to run;

To run on 27017 locally use:
```bash
docker run -p 27017:27017 -d mongo
```

### What is a Docker image?
- An image defines a Docker Container
  - Similar in concept to a snapshot of a VM
  - or a class vs an instance of the class
- Images immutable
  - once built, the files making the image do not change

### Image Layers
- Images are built in layers
- Each layer is an immutable file, but is a colleciton of files and directories
- Layers receive an ID, calculated via a SHA 256 hash of the layer contents
  - Thus if the layer contents change the SHA 256 hash changes also

```bash
sudo docker inspect mongo
[
    {
        "Id": "sha256:dcfda10b61c5f8c18ca946b8356309ba1b400509782a14321d9b619db6e51423",
        "RepoTags": [
            "mongo:latest"
        ],
        "RepoDigests": [
            "mongo@sha256:a4f2db6f54aeabba562cd07e5cb758b55d6192dcc6f36322a334ba0b0120aaf1"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2023-03-04T00:24:53.88530772Z",
        "Container": "5daec57c54165f501a519f77bc2f937a504aa2f9110118ea007d140e212a4feb",
        "ContainerConfig": {
            "Hostname": "5daec57c5416",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "27017/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.16",
                "JSYAML_VERSION=3.13.1",
                "MONGO_PACKAGE=mongodb-org",
                "MONGO_REPO=repo.mongodb.org",
                "MONGO_MAJOR=6.0",
                "MONGO_VERSION=6.0.4",
                "HOME=/data/db"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"mongod\"]"
            ],
            "Image": "sha256:171e0e822c39a141da57449760667f2c359fe1df60d75d93bc9b74bd36a6ae28",
            "Volumes": {
                "/data/configdb": {},
                "/data/db": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "DockerVersion": "20.10.23",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "27017/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.16",
                "JSYAML_VERSION=3.13.1",
                "MONGO_PACKAGE=mongodb-org",
                "MONGO_REPO=repo.mongodb.org",
                "MONGO_MAJOR=6.0",
                "MONGO_VERSION=6.0.4",
                "HOME=/data/db"
            ],
            "Cmd": [
                "mongod"
            ],
            "Image": "sha256:171e0e822c39a141da57449760667f2c359fe1df60d75d93bc9b74bd36a6ae28",
            "Volumes": {
                "/data/configdb": {},
                "/data/db": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 644622539,
        "VirtualSize": 644622539,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/8b711dbe275b6d06a094ff871fdb2dfbb353de63bf17c8970f9ee663f533c05f/diff:/var/lib/docker/overlay2/6d02500cf7bc7b4dcf90f171ecbe4fee61213721b4f625980398e5fefe11f007/diff:/var/lib/docker/overlay2/78606176e261836227fe8f310040225d50a5bfd193983683d5b31e87cdb40a56/diff:/var/lib/docker/overlay2/5a1ea89770fcf5de7e7f4e37d53e8c663bb24cab902690e8cfa92235da590bc6/diff:/var/lib/docker/overlay2/6e62fb1a9e8672055f3234d85f3069e2e6b658d27226fa882343adbe462bc245/diff:/var/lib/docker/overlay2/f283579bc2ed63d885a2e37be34d1617029bdab44b4627339be6e3d6f58c7b28/diff:/var/lib/docker/overlay2/4febeedd7a65fd3ed3c2a510e1195912061fea0cba301bfbaf1bee8ded144182/diff:/var/lib/docker/overlay2/1c8ede8d89236f07d1a0607c33b18f78cda6b65f1121242f3e33336badf9e6c0/diff",
                "MergedDir": "/var/lib/docker/overlay2/a1a5cd8c42d59d3b198307ab059e6b133697ea40a558bf283f5f526c8a12812c/merged",
                "UpperDir": "/var/lib/docker/overlay2/a1a5cd8c42d59d3b198307ab059e6b133697ea40a558bf283f5f526c8a12812c/diff",
                "WorkDir": "/var/lib/docker/overlay2/a1a5cd8c42d59d3b198307ab059e6b133697ea40a558bf283f5f526c8a12812c/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:202fe64c3ce39b94d8beda7d7506ccdfcf7a59f02f17c915078e4c62b5c2ed11",
                "sha256:ab968d9beeca3e673f2c1da5127e64001f533e67621c5bdda8b199e52644d481",
                "sha256:574dbd7fec5851505dae0575e59aabf3cbf0400daeef63decd948296aeee8fe8",
                "sha256:4f4db5266052f93ac320eae747090a0942b84015de0f6f77b454733a6f65c864",
                "sha256:5fa826358921c4fe391b4f009640117cacca4a2ada4b41d518540f1cd22f0917",
                "sha256:e177f1aba12348b811397dc38ea17d65ae581643df891a3ba53c7dfef3d27463",
                "sha256:e98061662eb572b66a1a69bfbef6a2cbf7d32080ebf2f43d5431cf24409c951b",
                "sha256:7582722f809f652734f8b39d8ac95c0d71de73ad294cc8fed7e31272d2a790ad",
                "sha256:d20b3746cdff8f117131424aa1c419fe326e8c5dea0d7d338475d09cf7ace085"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```
Layers are shown at the bottom of the meta data

### Image IDs
- Image Ids are a SHA 256 hash derived from the layers
  - Thus if the layers of the image changes the SHA 256 hash changes
- The Image ID listed by docker commands (ie 'docker images') is the first 12 characters
of the hash

### Image Tag Names
- The hash values of the images are referred to by tag names

### Image tag names
- The format of the full tag name is: [REGISTRYHOST/][USERNAME/]NAME[:TAG]
- For Registry Host 'registry.hub.docker.com' is inferred
- For :TAG -latest is default and inferred
- Full tag example: registry.hub.docker.com/mongo:latest


