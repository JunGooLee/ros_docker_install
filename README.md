## ROS with Docker
  
- Use ROS melodic (18.04) on Ubuntu 20.04 (Focal Fossa)
- Reference
> http://wiki.ros.org/docker   
> http://wiki.ros.org/docker/Tutorials
---

### Install ```Docker```
Follow this guide https://docs.docker.com/engine/install/ubuntu/ 
 

#### Manage Docker as a non-root user
1. Create the docker group.
```
$ sudo groupadd docker
```

2. Add your user to the docker group.
```
$ sudo usermod -aG docker $USER
```

3. Activate the changes to groups:
```
$ newgrp docker 
```

### Install ROS Docker
Follow this guide http://wiki.ros.org/docker/Tutorials/Docker

1. Pulling ROS melodic official images.
```
$ docker pull osrf/ros:melodic-desktop-full
```
<br/>

2. Run
```
$ docker run -it --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="$HOME/rosDoker:/root" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --net=host osrf/ros:melodic-desktop-full
```
- ```--net=host``` Use same port as host for ROS share
- ```--volume="$HOME/rosDoker:/root"``` Directory sharing options with host
- extra option : GUI
<br/>

3. Start with GUI

- adjust the permissions for GUI
```
$ xhost +local:root
```

- first terminal
```
$ docker start -ai {docker_name}   
```

- additional terminal
```
$ docker exec -it {docker_name} bash
```
```
$ source ros_entrypoint.sh
```


 
 ### Additional settings
 gedit ~/.bashrc 
 ```
alias ds='docker start -ai {docker names}'
alias de='docker exec -it {docker names} bash'
alias dg='docker images'        # Print image list 
alias da='docker ps -a'         # Print all container list 
alias dc='xhost +local:root'    # GUI option
 ```
 
 - Docker command reference
 https://docs.docker.com/engine/reference/commandline/run/
 
