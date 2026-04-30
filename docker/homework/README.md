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

## Hands-On–  Dinner Suggestion
- Prepare a Dockerfile base on app  **Dinner Suggestion**
- Run build in order to create image
- Set a tag
- Push the image into your Docker Hub

### Bouns practie
- Run the app locally before
- change the expose port to 5001
- Set the expose port as argument
  - For Example
```
py.exe app.py
http://127.0.0.1:5000/
```
- Set the expose port as argument
  - For Example
```
# (Optional) Use it to start your application
# ENV APP_PORT=$PORT
# CMD ["sh", "-c", "my-app --port $APP_PORT"]
```
