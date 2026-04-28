# Hands-On – Lab-02 Docker commands based on httpbin
- Docker run httpbin
- Practice stop,start, top, stat, inspect container and image, logs
- practice commit
- practice cp tag and push
- practice tag and push and save

```
docker run --name http_error -d -p 8990:80 kennethreitz/httpbin
http://localhost:8990/
docker stop <container id>
docker start <container id>
docker reststart <container id>

docker top <container id>
docker stats <container id>
docker inspect <container id>
docker image inspect 19bdfb32d22e | grep -i layer
docker logs --follow <container id>
docker logs <container id> | less


docker exec -it http_error bash
docker ps
docker ps -a
docker images
docker rm -f <container id>
docker rmi -f <container id>


# Docker Pull and run again in order to practice commit and save
docker run --name http_error -d -p 8990:80 kennethreitz/httpbin
docker exec -it http_error bash
# echo "fix bug 1010" > fix-bug1010.txt
ls
cat fix-bug1010.txt
exit
docker commit aef7717dea84 http_error:fix1010
docker ps
docker images | grep -i http                                                      # see two http images
docker run --name http_error_new -d -p 8900:80 5872ce97baad                       # docker run two diff container    
docker ps
docker rm -f <origin container not new>
docker run --name http_error -d -p 8990:80 kennethreitz/httpbin
docker ps
docker images | grep -i http
docker exec http_error ls -l | wc -l
docker exec http_error_new ls -l | wc -l                  # with new file

docker exec -it http_error_new bash
ls
docker cp <container id>:fix-bug1010.txt .               # docker cp CONTAINER:filename DEST_PATH  make sure to type dot


docker tag <image id> dinghy123/http_error:fix1010
docker images
docker push dinghy123/http_error:fix1010
docker save -o http_error.tar dinghy123/http_error:fix1010
ls

```





