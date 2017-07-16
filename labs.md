Boxboat Bootcamp Labs
#####################

Lab 1.1: Running Your First Docker Container
--------------------------------------------

In this lab, we will examine the Docker CLI and execute our first container

docker container ls
docker image ls
docker container run hello-world
docker container ls
docker container ls -a
docker image ls
docker container run -d -p 8080:80 --name nginx nginx
docker container ls
docker image ls
docker container stop nginx
docker container rm nginx

Lab 1.2: Bonus: Docker Container Exec
-------------------------------------

In this lab, we will learn how to interact with an already running Docker container

docker container run -d -p 8080:80 --name nginx nginx
docker container exec -it nginx bash
exit
docker container ls
docker rm $(docker kill nginx)

Lab 1.3: Run Your Second Docker Container
-----------------------------------------

In this lab, we will run Nginx and try to view the content in another container

docker container run -d -p "8080:80" --name nginx --network test nginx

Now, let’s run an Alpine container
Make sure we run it with a shell
Attach it to the test network

Figure out how to get the index.html from nginx

Lab 1.4: Re-Run Nginx With Content
----------------------------------

In this lab, we will run Nginx with the content of our local directory

docker container run -d -p "8080:80" --name nginx --network test nginx

What is missing from the above command? Volume mounts
Syntax: -v  /host/path:/container/path

Lab 1.5: Processes On The Host
------------------------------

In this lab, we will look at the processes running on the host

ps aux
docker run -d -p "8080:80" --name nginx --network test nginx
ps aux

Lab 2.1: Docker Volumes
-----------------------

In this lab, we will learn more about Docker volumes

Named Volumes:

docker volume ls
docker volume create myvolume
docker volume inspect myvolume
docker container run --rm -it -v myvolume:/myloc/tmp --name alpine alpine
touch /myloc/tmp/test.txt
exit
ls /graph/volumes/myvolume/_data

Host Volumes:

docker container run --rm -it -v /tmp:/myloc/tmp --name alpine alpine
touch /myloc/tmp/test.txt
exit
ls /tmp

Lab 2.2: Docker Networking
--------------------------

In this lab, we will get more practice with Docker networking

docker network ls
docker network inspect test

Put 2 containers on the same bridge network so they can communicate via DNS

Lab 2.3: Exposing and Publishing Ports
--------------------------------------

In this lab, we will learn about exposing and publishing ports

Exposing Ports:
Run Nginx without any port mapping
docker container ls

Publishing Ports:
Run Nginx and let Docker choose a high port
Run Nginx and choose the high port

For communication within the network, use the exposed port
For communication external to the network, use the published port

Lab 3.1: Dockerfiles
--------------------

In this lab, we will create a Dockerfile together and deploy a simple Python flask app
Go to the "simple-python-app" directory

To deploy Python code, we need to do a few things

1. Select a base image
2. apt-get update
3. Install dependencies (python-pip python-dev build-essential)
4. Create a working directory
5. Copy our application code
6. Install our requirements
7. Expose our application port (5000)
8. Set the default command

Now, we build and test:

docker build -t flask-app:latest .

Lab 3.2: Advanced: Multi-Stage Builds
-------------------------------------

In this lab, we will show how Multi-Stage Builds can reduce application size

Go to to multi-stage-builds directory
In here, we have 2 subdirectories, small and large
Each subdirectory contains a dockerfile, let's build them and compare

Lab 4.1: WordPress
------------------

In this lab, we will launch the WordPress application.
It contains 2 components: front-end (PHP) and backend (database)

First, we'll create the proper network: 
	wordpress-net

Next, we will create 2 volumes:
	db-data
	wordpress-data

Next, we will launch the database container	
Create a docker container run command with the following configuration:
	name: db
	container: mysql:5.7
	volumes: db-data:/var/lib/mysql
	network: wordpress-net
	environment variables:
		MYSQL_ROOT_PASSWORD: wordpress
      	MYSQL_DATABASE: wordpress
      	MYSQL_USER: wordpress
      	MYSQL_PASSWORD: wordpress

Next, we will launch the WordPress container
Create a docker container run command with the following configuration:
	name: wordpress
	container: wordpres:latest
	volumes: wordpress-data:/var/www/html
	network: wordpress-net
	ports: 8001:80
	environment variables:
		WORDPRESS_DB_HOST: db:3306
      	WORDPRESS_DB_PASSWORD: wordpress
