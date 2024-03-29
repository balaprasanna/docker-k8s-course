#  Docker - k8s course

### Section 1: Docker
### Section 2: K8S


#### Step 1: Create droplet and add docker to it with docker machine

Create the following env variables 
`$DO_TOKEN` `$SIZE` `$REGION`
using `doctl`
  
```
docker-machine create --driver digitalocean --digitalocean-access-token=$DO_TOKEN --digitalocean-size $SIZE --digitalocean-region $REGION dockerbox
```

Out => Expected output:
```
Creating CA: /home/bala/.docker/machine/certs/ca.pem
Creating client certificate: /home/bala/.docker/machine/certs/cert.pem
Running pre-create checks...
Creating machine...
(dockerbox) Creating SSH key...
(dockerbox) Creating Digital Ocean droplet...
(dockerbox) Waiting for IP address to be assigned to the Droplet...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env dockerbox

```
---

$ docker-machine ls
```
NAME        ACTIVE   DRIVER         STATE     URL                        SWARM   DOCKER     ERRORS
dockerbox   -        digitalocean   Running   tcp://165.22.48.219:2376           v19.03.2   
```

#### Step 2: Jump inside the DO Droplet / machine

```
$ docker-machine ssh dockerbox
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-157-generic x8664)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

29 packages can be updated.
12 updates are security updates.

New release '18.04.2 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


root@dockerbox:~# ls
root@dockerbox:~# docker -v
Docker version 19.03.2, build 6a30dfc

```

#### Step 3: Run helloworld docker container

```
root@dockerbox:~# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:451ce787d12369c5df2a32c85e5a03d52cbcef6eb3586dd03075f3034f10adcd
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

```

---

#### Tips: Copy files from local to docker-machine

Example : copy the local src folder recursively into docker-machine's /tmp folder
```
docker-machine scp -r src/ dockerbox:/tmp
```


#### Optional: Connect local docker cli --- to --- remote machine's docker engine

1. Print out the docker ENV config for the remote docker-machine 
```
$ docker-machine env dockerbox
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://165.22.48.219:2376"
export DOCKER_CERT_PATH="/home/bala/.docker/machine/machines/dockerbox"
export DOCKER_MACHINE_NAME="dockerbox"
# Run this command to configure your shell: 
# eval $(docker-machine env dockerbox)
(base) bala@issadmin-Alienware-Aurora-R7:~/Desktop/CFDSA
```

2. Eval the docker env to point local docker client to Remote docker-machine
```
$ eval $(docker-machine env dockerbox)
(base) bala@issadmin-Alienware-Aurora-R7:~/Desktop/CFDSA
(base) bala@issadmin-Alienware-Aurora-R7:~/Desktop/CFDSA
$ docker -v
Docker version 19.03.1, build 74b1e89

```

#### rm the digital ocean docker-machine
```
$ docker-machine rm dockerbox
About to remove dockerbox
WARNING: This action will delete both local reference and remote instance.
Are you sure? (y/n): y
Successfully removed dockerbox
```
