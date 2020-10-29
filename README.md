# Traefiq (Angular and NODEjs services)
Reverse proxy complete Setup

### **Getting Started**

All the configurations that i have perfomed are based on Ubuntu Machine. Make sure Docker is installed.

### **Steps**

#### Step 1

Copy your source code to your server machine. I chose to have the path as below:

```
mkdir /home/code
cd /home/code
```

#### Step 2

I copied Frontend app and backend server code that includes its own Dockerfile.

```
/home/code/ApiServer/
/home/code/Frontend/
```

#### Step 3

Create another directory to place reverse proxy configurations.

```
/home/code/docker/
```

#### Step 4

Create network on which docker services could run and interact over if in case.

```
sudo docker network create --driver=overlay web
```

**web** is the network that is referred in the docker-compose file.

#### Step 5
Make sure you check .env file and fill in the right values. 

#### Step 6

Make sure docekr-compose.yml file is placed parallel to your Source code.

```
/home/code/ApiServer/
/home/code/Frontend/
/home/code/docker/
/home/code/docker-compose.yml
```

Build the images
```
docker-compose build
```

#### Step 7

Deploy to swarm using below command.

```
docker stack deploy -c <(docker-compose -f  docker-compose.yml  config) NAME_OF_YOUR_STACK
docker stack ls
```

#### Step 8

Check if services are up:

```
docker stack services NAME_OF_YOUR_STACK
docker stack ps NAME_OF_YOUR_STACK
```

Based on the configurations specified in docker-compose together with static traefiq.yml file the domain certificates for HTTPS using LetsEnctypt would be created. Based on your frontend rule mapping you should be able to access your services over https without any port numbers.

You can increase replicas of your services by just logging ino portainer and manage your services.

Finally Frontend and Backend services run on the ports specified in .env within the container. This has specifid in docker-compose and passed as an arg to Dockerfile to build.


#### Step 9

```
web.<YOUR_DOMAIN>
api.<YOUR_DOMAIN>
portainer..<YOUR_DOMAIN>
```
