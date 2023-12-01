# Caldera Container  

#### Ubuntu Docker Install  
```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```  

##### Execute Docker w/o Sudo
```
sudo usermod -aG docker [USERNAME]
su - [USERNAME]
groups
sudo usermod -aG docker [USERNAME]
```

##### scp Dockerfile to machine
```
scp /location/of/file/on/local/Dockerfile [USERNAME]@[DEST_IP]:/home/[USERNAME]/
```

##### To build the Docker image w/o OT Plugins run the following:[^1]
```
sudo docker build --no-cache --build-arg WIN_BUILD=true -t caldera:latest .
```

##### w/ OT Plugins
```
docker build --no-cache --build-arg WIN_BUILD=true --build-arg OT_BUILD=true -t caldera:latest .
```

##### To start the container run the following:
```
sudo docker run -d --name calderaserver -p 8888:8888 caldera:latest
```

To access Caldera once running, open a browser and navigate to ```[HOST_IP]:8888```

### Troubleshooting
Check that image was created
```
sudo docker image ls
```
Delete Docker image
```
sudo docker image rm [image_name]
```
Check if container is running
```
sudo docker ps
```
Stop container
```
sudo docker stop [container_name]
```
Remove Container and verify it was removed
```
sudo docker rm [container_name]
sudo docker ps -a
```

> There are three users: red, blue, and admin  
> To change their passwords modify the appropriate lines in default.yml  
> The default password for all is 'admin'

[^1]: The build file must be named Dockerfile or the build will fail.  The build command must also be run in the same directory as the Dockerfile.


