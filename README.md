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

Docker Volumes


# Manage data in Docker
By default all files created inside a container are stored on a writable container layer. This means that:  
The data doesn’t persist when that container no longer exists, and it can be difficult to get the data out of the container if another process needs it.

To list out existing volumes 
  ```sh 
  docker volume ls
  ```
   #### to create a container for stateless applications 
  ```sh
  docker run -it --name vtuatjenkins01
  ```
Docker has 3 options for containers to store files in the host machine, so that the files are persisted even after the container stops:

Docker Volume Types
1. anonymous volumes
1. named voluems
1. host volume or bind volumes
 
Anymous Volumes

Create a container with an anonymous volume which is mounted as `/data01` on container. in this case we mention container directory name. On host system it maps to a random-hash directory under /var/lib/docker directory. 
  ```sh 
  docker run -it --name vtwebuat01 -v /data01 nginx /bin/bash
  ```
On Host to verify volume 
  ```sh
  docker volume ls 
  docker inspect <volume_name>
  ```

Named Volumes 

Create a container with a named volume name which is mounted as `/data01` on container. You can see volume name as `vtwebuat02_data01_val`
  ```sh 
  docker run -it --name vtwebuat02 -v vtwebuat02_data01_val:/data01 nginx /bin/bash
  ```
Create a named volume then attach volume to a container 
  ```sh 
  docker volume create vtuatweb03_data01_vol
  docker run -it --name vtuatweb03 -v vtuatweb02_data01_vol:/data01 nginx /bin/bash
  ```

Create a named volume with size 
  ```sh
  docker volume create --opt o=size=100m --opt device=/data3 --opt type=btrfs vtuatdb02_data3 // to create volume with size 
  ```

 Host Volumes 

Create a host volume 
  ```sh 
  mkdir /opt/data02
  docker run -it --name vtwebuat03 -v /opt/data02:/data02 nginx /bin/bash
  ```
 **
 Docker commands to DEBUG, LOG, Resource utilization (CPU, memory, disk) by docker running container. 
 
 Running docker stats on all running containers against a Linux daemon.
 
 docker stats :- Shows the memory utilization, CPU, memory disk of running containers
 
 docker stats container_name container_id :- shows the stats of specific container.
 
 docker stats --all --format "table {{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}" container_name container_name :- Shows the stats in table format
 
 docker log container_name :- Shows the logs of the container
 
 docker -D info :- debug
 
 Docker Logs Location in Linux
 
Ubuntu 	/var/log/upstart/docker.log

Boot2Docker 	/var/log/docker.log

Debian1 	/var/log/daemon.log

Systemd based OSes (CoreOS, SUSE, Fedora, CentOS, Red Hat Enterprise  	journalctl -u docker.service
___________________________________________________________________________________________________________________________________________________________________________________

 **Kubectl Commands**
 
 kubectl get svc 
 
 kubectl get pods
 
 kubectl apply -f app_name
 
 kubectl top [flags] [options]  kubectl top nodes, pods              Display Resource (CPU/Memory/Storage) usage.
 
 kubectl logs -c -p -f container_name
 
 kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
 
 kubectl get deployment metrics-server -n kube-system
 
 **Debugging Pods**
 
 kubectl describe pods ${POD_NAME}
 
** **My pod stays pending
If a pod is stuck in Pending it means that it can not be scheduled onto a node. Generally this is because there are insufficient resources of one type or another that prevent scheduling. Look at the output of the kubectl describe ... command above. There should be messages from the scheduler about why it can not schedule your pod.
 **
 **
 
  
  
 
 
 
 
 

**



