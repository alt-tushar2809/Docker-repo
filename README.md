# Docker-repo
 Docker Installation on Centos
 
# Installing Docker on Amazon Linux server

1.Update packages
```sh 
yum update -y
```
2.Install docker
```sh 
yum install docker -y
```

# Docker Installation on CentOS server
##### Referance URL : https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository
### PREREQUISITES

Please follow below steps to install docker CE on CentoOS server instance. For RedHat only Docker EE available 

1.Install required packages.

```sh 
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
  
  ```
  
2.Use the following command to set up the stable repository.
 
 ```sh 
 sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### INSTALLING DOCKER CE

1.Install the latest version of Docker CE.
```sh 
sudo yum install docker-ce
```

If prompted to accept the GPG key, verify that the fingerprint matches 
060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35, and if so, accept it.

2.Start Docker.
```sh 
sudo systemctl start docker
```

3.Verify that docker is installed correctly by running the hello-world image.
```sh
sudo docker run hello-world
```

Docker Commands 


1. how to search a docker image in hub.docker.com
```sh
docker search httpd
```
2. Download a docker image from hub.docker.com
```sh
docker image pull <image_name>:<image_version/tag>
```

3. List out docker images from your local system
```sh
docker image ls
```

4. Create/run/start a docker container from image
```sh
docker run -d --name <container_Name> <image_name>:<image_version/tag>

d - run your container in back ground (detached)
```

5. Expose your application to host server
```sh
docker run -d  -p <host_port>:<container_port> --name <container_Name> <image_name>:<Image_version/tag>

docker run -d --name httpd_server -p 8080:80 httpd:2.2
```

6. List out running containers
```sh
docker ps
```

7. List out all docker container (running, stpooed, terminated, etc...)
```sh
docker ps -a
```

8. run a OS based container which interactive mode (nothing but login to container after it is up and running)

```sh
docker run -i -t --name centos_server centos:latest
i - interactive
t - Terminal
```

9. Stop a container 
```sh
docker stop <container_id>
```

10. Start a container which is in stopped or exit state

```sh
docker start <container_id>
```
11. Remove a container

```sh
docker rm <container_id>
```

12. login to a docker container
```sh
docker exec -it <container_Name> /bin/bash
```

