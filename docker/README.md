# Installation of Docker Desktop 

# Hands-On – Lab-01 - Getting Started with Docker
**Installation:​**
  - Steps to install Docker on different platforms (Windows, macOS, Linux).​
  - Basic Commands:
  - docker --version​
  - docker run hello-world​
  - docker ps​
  - docker images

**Bonus Questions**
- Find the commands of LXC Provides Independence & Implemented Using​
- Run command on both cli (cmd ipconfig, wsl ip addr) why its diff ?  

## Solution:

- Go to the link and install it step by step following the instruction:
  https://docs.docker.com/desktop/install/windows-install/
- Go to the cli of WSL and check the version of Docker
```
docker info
docker version
```

## Basic Docker commands:
```
docker ps
docker ps -a
docker images
```

### Docker pull hello-world
- Open the cli of WSL and Pull your first image
  
```
docker pull hello-world
```

- Go to https://hub.docker.com/_/hello-world -> Shared Tags -> latest:linux
in order to see the Dockerfile
- **It is just prompt via cli hello-world**

#### Hands-On – Lab-02 monopoly game
- Docker pull and run the monopoly game on one command​
- Browse via Google Chrome​
- Display the images​
- Display the container run time and exited

##### Solution: monopoly game
```
docker run -it --name monopoly_8443 -p 8443:8443 gonzague/monopoly
https://localhost:8443/
docker images
docker ps -a
```


