Boxboat Bootcamp Labs
---------------------

5.1: Voting App Docker Compose
--------------------------

This lab will introduce the Docker Compose tool  
We will spin up the Voting App using Docker Compose
It won't quite work, but we'll see a lot of docker-compose.yml file contents

Navigate to docker-compose-lab/voting-app  
execute `docker-compose up -d` 

5.2: WordPress Docker Compose
-----------------------------

This lab will help us create compose files from scratch
We will launch WordPress using docker-compose  

Navigate to docker-compose-lab/wordpress 
You will **only** need to create a docker-compose.yml file, not anything else

Create a docker-compose.yml file with the following configuration:  

```
networks:   
  wordpress-net  

volumes:  
  db-data
  wordpress-data  

Database container  
  service name: db  
  image: mysql:5.7  
  volumes: db-data:/var/lib/mysql  
  network: wordpress-net  
  environment variables:  
    MYSQL_ROOT_PASSWORD: wordpress
    MYSQL_DATABASE: wordpress
    MYSQL_USER: wordpress
    MYSQL_PASSWORD: wordpress

WordPress container
  service name: wordpress
  depends on: db
  image: wordpress:latest
  volumes: wordpress-data:/var/www/html
  network: wordpress-net
  ports: 8001:80
  environment variables:
    WORDPRESS_DB_HOST: db:3306
    WORDPRESS_DB_PASSWORD: wordpress
```
