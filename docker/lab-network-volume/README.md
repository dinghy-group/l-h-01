# Docker Network and Volume
## Docker Network
### Hands-On - Docker network - Two diff bridge mynet
- Creating new network
- Launching containers in different bridges
- Launch two containers nt01 and nt02 in default bridge network
- Launch two containers nt03 and nt04 in mynet bridge network
- Go into nt01 container and ping to nt02 or nt03
- Go into nt01 container and ping to nt03 or nt04

```
docker network create -d bridge mynet
docker network inspect mynet
```
- Launch two containers nt01 and nt02 in default bridge network
```
docker container run -idt --name nt01 alpine sh
docker container run -idt --name nt02 alpine sh
```

- Launch two containers nt03 and nt04 in **mynet** bridge network

```
docker container run -idt --name nt03 --net mynet alpine sh
docker container run -idt --name nt04 --net mynet alpine sh
```

- lets examine if they can interconnect

```
docker exec nt01 ifconfig eth0
docker exec nt02 ifconfig eth0
docker exec nt03 ifconfig eth0
docker exec nt04 ifconfig eth0
  # OutPut
nt01 = 172.17.0.4  
nt02 = 172.17.0.5  
nt03 = 172.22.0.2  
nt04 = 172.22.0.3  
```

- Go into nt01 container and ping to nt02 
- Go into nt01 container and ping to nt03 or nt04
```
docker exec -it nt01 sh
#ping <IP nt02>
success
#ping <IP nt03>
not success, since its diff bridge
```
### Hands-On - backend and frontend
backend



- Dispaly and create bridge
```
docker network ls
docker network inspect bridge
docker network create devops-net
docker network ls
```

- Run first container (backend)
```
docker run -d \
  --name backend \
  --network devops-net \
  nginx
```

- Run second container (frontend)

```
docker run -d \
  --name frontend \
  --network devops-net \
  busybox \
  sleep 3600
```

- Test container-to-container communication and display
  - Subnet, Gateway, Connected containers, IPs assigned automatically
```
docker exec -it frontend sh
  # Inside container:
ping backend
  # Exit
docker network inspect devops-net
```

- Connect running container to another network
```
docker network connect bridge frontend
```

- Now frontend has 2 network interfaces.

```
docker inspect frontend
```
- Disconnect from a network and clean up
```
docker network disconnect bridge frontend
docker rm -f frontend backend
docker network rm devops-net
```

## Docker Persistent Volume

### Types of volumes
- automatic volumes  - is not persisting data, hard to reuse volume and data back
- named volumes
- volume binding
  
#### Automatic Volumes - Do it with WSL
```
docker container run  -idt --name vt01 -v /var/lib/mysql  alpine sh
docker images
docker ps
docker inspect vt01 | grep -i mounts -A 10
```
#### Named volumes - Do it with WSL

```
docker container run  -idt --name vt02 -v db-data:/var/lib/mysql  alpine sh
docker inspect vt02 | grep -i mounts -A 10
```

#### Volume binding -  Do it with WSL
```
sudo -s mkdir /root/sysfoo
sudo -s chmod 777 /root/sysfoo
docker container run  -idt --name vt03 -v /root/sysfoo:/var/lib/mysql  alpine sh
docker inspect vt03 | grep -i mounts -A 10
sudo -s ls /root/sysfoo
pwd
sudo -s touch /root/sysfoo/file1.txt
sudo -s ls /root/sysfoo
sudo chmod 777 /root/sysfoo
docker ps
docker exec -it vt03 sh
ls /var/lib/mysql
  #You should see:
file1

# Test
docker rm -f a56862f350e2
sudo -s ls /root/sysfoo         # still exsit
docker container run  -idt --name vt03 -v /root/sysfoo:/var/lib/mysql  alpine sh
sudo -s touch /root/sysfoo/file2.txt    # on host 2 files
sudo -s ls /root/sysfoo 
docker exec -it vt03 sh
cd var/lib/mysql                      # dind inside 2 files
ls 
  # You should see:
file1 file2

```

#### See volumes commands and cleanup

- Create a volume
- List all volumes
- Inspect details
- Remove a volume
- Clean up unused volumes
```
docker volume create my-vol
docker volume ls
docker volume inspect my-vol
docker volume rm my-vol
docker volume prune

docker rm -f vt01 vt02 vt03
docker volume rm db-data
```



## Solution: mysql Persistent Volume on top of Docker Host = Local PC
- **Note** - Do it via WSL cli
```
mkdir -p mysql-data
chmod 777 mysql-data

docker run -d \
  --name mysql \
  -p 33306:3306 \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=mySchema \
  -v /home/dinghy/mysql-data:/var/lib/mysql \
  mysql:5
  
  docker exec -it mysql mysql -uroot -psecret -e "SHOW DATABASES;"
  docker exec -it mysql mysql -uroot -psecret -e "CREATE DATABASE testDB;"
  CREATE DATABASE testDB;
  
  sudo -s cd /home/dinghy/
  
  
docker ps
docker rm -f 06714f536d3f
docker images
docker rmi -f 5107333e08a8

ls
cd mysql-data/
ls

run again

docker run -d ......etc...
docker exec -it mysql mysql -uroot -psecret -e "SHOW DATABASES;"

see the testDB

```


