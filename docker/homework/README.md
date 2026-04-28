# Installation Jenkins based on Docker
-  Install Jenkins lts version
-  config till you getting the first page of jobs
-  create freestyle job
  
  - which including bash script with output **hello-world**


### Build a new Image via Dockerfile base on nodejs and jenkins images

- Create a app.js Application based of Node which running ​
- res.end('Hello, World!\n');​
- Wrap it with dockerfile​
- Build an image​
- Run the image​
- Go to the app via the via the Browser​
- Test the node version via interactive mode​
- Tag, Push and verify the Image in Docker Hub

### Solution: Build a new Image via Dockerfile base on nodejs and jenkins images

- Download the Dockerfile
- Build Time run the command below in order to create new local image

```
docker build -t jenkins-with-nodejs:1.0 .
docker images
docker images | awk '{print $1}'
```

- Run time run the command below in order to run the docker on backround

```
docker run -d --name jenkins -p 8080:8080 jenkins-with-nodejs:1.0
docker ps
```

- Go the the browser and make sure the login page of Jenkins is running http://127.0.0.1:8080
- Get jenkins password via command

#### Fix Error via WSL
- Open the cli of WSL and type the command below, it is not work with cli of Git Bash

```
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

#### Create First Admin User
- Username = admin
- Password = admin
- Full name = admin
- E-mail address = admin@admin
- Go into Docker shell

```
docker run -it jenkins-with-nodejs:1.0 /bin/bash
cd /usr/local/bin/
node -v
```

