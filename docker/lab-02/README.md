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


