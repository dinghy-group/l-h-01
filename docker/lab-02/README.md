# Hands-On – Lab-02 mysql db Basic Commands​
- Docker pull mysql​
- Docker run with port 3406​
- List of all images​
- Go inside a running mysql container​
- Go to Cli of mysql and show all database
- select * from user


## Solution: mysql Docker pull & Docker run & deep dive via the interactive mode

```
docker pull mysql
docker run --name test-mysql -e MYSQL_ROOT_PASSWORD=strong_password -d mysql
docker run --name test-mysql -p 33306:3306 -e MYSQL_ROOT_PASSWORD=strong_password -d mysql

   #Run mysql tag version 5  
docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=mySchema mysql:5
docker exec -it mysql bash
docker exec -it test-mysql bash
mysql -u root -p
strong_password
use mysql;
show tables;
select * from user
select User from user;
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


## Additinal Example keep the files - Docker Persistent Volume

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



