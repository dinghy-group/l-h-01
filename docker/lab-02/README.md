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

