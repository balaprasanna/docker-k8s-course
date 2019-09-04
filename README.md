# docker-k8s-course


Step 1: Create droplet and add docker to it with docker machine

```
docker-machine create --driver digitalocean --digitalocean-access-token=$DO_TOKEN --digitalocean-size $SIZE --digitalocean-region $REGION dockerbox
```
