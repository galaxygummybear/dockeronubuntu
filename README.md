# Guide on installing Docker Daemon on Ubuntu 23.04


## Remove existing packages
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

## Set up Docker's Apt repository.
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## Install the Docker packages
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## After installing the most important step is to `enable` docker
```bash
sudo systemctl enable docker
```

## Then you can run Docker Daemon with the `dockerd` command.
```bash
sudo dockerd
```

## Finally on another terminal, do your docker stuffs.
```bash
sudo docker run --rm --gpus all -it -p 8000:8000 <username>/<pkg_name>:latest-gpu
```



###### *Important Note : Running Docker Desktop on ubuntu is very unstable. It will throw this error: `libnvidia-ml.so.1: cannot open shared object file`. Just use the Docker Daemon.

## To Stop all containers:
```bash
sudo docker stop $(sudo docker ps -a -q)
```

## Remove all containers:
```bash
sudo docker rm $(sudo docker ps -a -q)
```

## Remove all images:
```bash
sudo docker rmi $(sudo docker images -q)
```

## Remove all volumes:
```bash
sudo docker volume prune
```

## Remove all networks:
```bash
sudo docker network prune
```

## Clear Docker cache:
```bash
sudo docker builder prune --all --force
```
