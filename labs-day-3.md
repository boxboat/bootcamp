Boxboat Bootcamp Labs
=====================

Lab 6.1: Build your own Docker Swarm cluster
---------------------------------------------

Navigate to `play.boxboat.net`, and create a new instance

Now, we execute `docker swarm init`
This won't work, we need to specify the listen address

Now, copy that line (`docker swarm join...`), create a new instance, and execute it in that shell

Lab 6.2: Creating Docker Swarm Services
---------------------------------------

`docker service create --name alpine --replicas 3 alpine`
Creates a new Docker Swarm service called "alpine," with 3 replicas

`docker container run -d --replicas 3 --name hello-world --p 10080:80 tutum/hello-world`
Creates a new Docker Swarm service that runs in the background, with 3 replicas, called "hello-world," and publishes port 10080 to internal port 80

Lab 6.3: Wordpress in Docker Swarm
----------------------------------

Edit `../bootcamp/docker-swarm-lab/wordpress/docker-compose.yml` to deploy 1 replica of each service, and set a restart policy to `on-failure`.


