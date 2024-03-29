# Dockerizing-a-Django-Web-With-mySql
# Table of Contents

- [Prerequisites](#prerequisites)
- [How to Build](#how-to-build)
- [Configuration](#configuration)

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
    docker network create --subnet 10.0.0.0/24 custom-network
    ```
 3. Run the MySQL container:

    ```bash
    docker run -d --network custom-network --ip 10.0.0.15 --hostname mysql-database -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=djangodb mysql
    ```
