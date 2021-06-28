## Start all machines with Vagrant
`vagrant up`

It might take a while as it downloads the dependencies after provision completed run the following command to list all machines.
`vagrant status`


### Login into manager01 with the following command and verify Docker
```
vagrant ssh manager01
docker info
```


### Init Docker Swarm in manager01
```
docker swarm init --listen-addr 172.17.149.2:2377 --advertise-addr 172.17.149.2:2377
```

### create new swarm with the same dataset
```
docker swarm init --force-new-cluster
```

### Run the following command to get the token to join manager
```
docker swarm join-token manager
```


### Deploy Portainer
```
curl -L https://downloads.portainer.io/portainer-agent-stack.yml -o portainer-agent-stack.yml

docker stack deploy --compose-file=portainer-agent-stack.yml portainer
```

### list all containers from all nodes 
```
 docker node ps $(docker node ls -q)
```


### Deploy NGINX
```
docker service create --name my_nginx --replicas 5 --publish published=8080,target=80 nginx
```


### Testing Time
Navigate to http://localhost:8080/ to verify Nginx, and navigate to http://localhost:9000/ to open Portainer, lastly. navigate to http://localhost:9000/#/swarm/visualizer to visualize all your applications.