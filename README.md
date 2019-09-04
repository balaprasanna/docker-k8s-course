# docker-k8s-course


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
Welcome to Ubuntu 16.04.6 LTS (GNU/Linux 4.4.0-157-generic x86_64)

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


