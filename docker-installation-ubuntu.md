# Installation methods
You can install Docker Engine in different ways,this instruction details the steps of installing Docker from Docker's apt repository.
For other methods, refer to [here](https://docs.docker.com/engine/install/ubuntu/)

## Install using the apt repository

1. Set up Docker's apt repository.
```
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
2. Add the repository to Apt sources:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Note

If you use an Ubuntu derivative distribution, such as Linux Mint, you may need to use UBUNTU_CODENAME instead of VERSION_CODENAME.

3. Install the Docker packages.

Latest Specific version
To install the latest version, run:
```
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verify that the installation is successful by running the hello-world image:
```
 sudo docker run hello-world
```
This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

