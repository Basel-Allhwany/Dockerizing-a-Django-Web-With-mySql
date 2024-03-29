# Dockerizing-a-Django-Web-With-mySql
# Table of Contents

## [Prerequisites](#prerequisites)        |  [How to Build](#how-to-build)      |    [Configuration](#configuration)

## Prerequisites

Before starting, ensure you have the following prerequisites installed:

- Docker
- Docker Compose

## How to Build

1. Clone the repository to your local machine:

    ```bash
    git clone https://github.com/Basel-Allhwany/Dockerizing-a-Django-Web-With-mySql.git
    cd Dockerizing-a-Django-Web-With-mySql
    ```
2. Create a network for container communication:

    ```bash
    docker network create --subnet 10.0.0.0/24 Docker-network
    ```
 3. Run the MySQL container:
    
    ```bash
    docker run -d --network Docker-network --ip 10.0.0.20 --hostname mysql-database -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=djangodb mysql
    ```
4. Build and run the Django container:

    ```bash
    cd Django
    docker build -t my-django .
    docker run -d --network Docker-network --ip 10.0.0.10 --hostname django my-django
    ```

5. Build and run the Nginx container:

    ```bash
    cd ../nginx
    docker build -t my-nginx .
    docker run -d --network Docker-network --ip 10.0.0.11 -p 80:80 --hostname nginx my-nginx
    ```

6. Migrate tables to the new database:

    ```bash
    docker exec -it <django_container_id> bash
    cd ~/mysite
    python3 manage.py migrate
    ```
   to Check tables in the MySQL container :

     ```bash
       docker exec -it <mysql_container_id> bash
       $ mysql -p
       > SHOW DATABASES;
       > USE djangodb;
       > SHOW TABLES;
    ```
7.Finally go to http://10.0.0.11 to Check The Connectivity  

![تصميم بدون عنوان](https://github.com/Basel-Allhwany/Dockerizing-a-Django-Web-With-mySql/assets/165336853/2aae53e9-2b46-4ce6-a410-c4e6697c4f79)                                       

    
## Configuration
- configure django settings by editting ./django/mysite/settings.py file
- The proxy pass and the server name can be configured by editting ./etc/nginx/conf.d/default.conf file
