# Swarm mode of Docker engine


## Reading

  For complete reference and key concept please refer (https://docs.docker.com/engine/swarm/key-concepts/). All instruction are based on the tutorial provided in docker site.  Though here are my notes. 

## Machine 

  Get three machine in with your favourite cloud provider. This POC uses digital ocean ( Ubuntu 14.04, 512 MB RAM, single CPU) machine. 
  
## First install docker (v1.12+)


    sudo apt-get update
    curl -fsSL https://test.docker.com/ | sh


## Start the swarm 

    docker swarm init --listen-addr <<swarm manager>>:2377

run “docker info” to get the swarm info

## On the worker machine, run the following command to join the swarm cluster 

    docker swarm join <<swarm manager>>:2377

## Once the worker have joined. Launch the containers. 

    docker service create --replicas 5 -p 32033:8080  --name service_name  <<image name >>

Once launched the application can be accessed at cluster machine(s) on following address, assuming Docker container is listening at 8080 port. And -p option maps the container port onto host port number. 

    http://<<any of the cluster machine ip>>:32033/

container instances can be scaled up or down with following command
docker service scale service_name =2

## if another machine has to be added as manager into the cluster.

    docker swarm join --manager --listen-addr <<current swarm mananger machine ip>>:2377 <<machine ip address>>:2377

## Swarm up and running 
