# Installation Jenkins based on Docker
-  Install Jenkins lts version
-  config till you getting the first page of jobs
-  create freestyle job
  
  - which including bash script with output **hello-world**


## **Jenkins installation base on Docker image**
- Work local server - PreRequsite is Docker desktop installed

```
docker run -d --name jenkins -p 8080:8080 jenkins/jenkins
  # See the logs in case its not work
docker logs 13d3a0adddb1
  # You should delete the docker container id of jenkins
docker rm -f <container id>
sudo curl ifconfig.me
```
- Go to the browser and open a new tab http://host-ip:8080
- in docker cli run the below command and insert to the jenkins password page

### Open the **cli of WSL** and type the command below, it is not work with cli of Git Bash

```
  # from Git bash
docker logs jenkins
  # from WSL we can use cat command as well
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

## Hands-On– Lab-03-01 Dockerfile Dinner Suggestion
- Run the app without dockerfile
```
py.exe app.py
http://127.0.0.1:5000/
```

- Run the app with dockerfile

```
docker build -t dinner_flask_lh_app .
docker images
docker run -d -p 5099:5000 dinner_flask_lh_app
http://localhost:5099/
```

- Docker tag, push and pull

```
docker images
docker ps
docker tag dinner_flask_lh_app dinghy123/dinner_flask_lh:latest
docker push dinghy123/dinner_flask_lh:latest
docker pull dinghy123/dinner_flask_lh:latest
```


