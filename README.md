## Setting Up PostgreSQL with Docker
### Introduction

PostgreSQL is a powerful, open-source object-relational database system. It is a highly scalable, SQL-compliant database management system that is used to handle large workloads. PostgreSQL is a popular choice for many developers and organizations due to its robust features, extensibility, and reliability.

In this tutorial, we will walk you through the process of setting up PostgreSQL on your system. In this modern age, you can take advantage of Docker to easily set up and run PostgreSQL on your local machine. Docker is a platform that allows you to package, distribute, and run applications in containers. It provides a lightweight and efficient way to run applications in isolated environments. Docker is available for Windows, macOS, and Linux, making it a versatile tool for developers.
Prerequisites

Before you begin, you will need to have the following prerequisites:

1. A system running Windows, macOS, or Linux
2. Docker installed on your system
3. Basic knowledge of using the command line

Once Docker is installed, you can verify the installation by running the following command in your terminal:

```
docker --version
```

This command will display the version of Docker installed on your system.
Setup

- Create a Data Directory: Now that you have Docker installed, create a new directory for your PostgreSQL data. This directory will be used to store the data files for your PostgreSQL instance. It's recommended to keep this directory in your project folder for easy management.

- Create a Docker Compose File: In the directory you created, create a new file named docker-compose.yml. This file will contain the configuration for your PostgreSQL container. Insert the following content into the docker-compose.yml file:

```
version: '3.8'

services:
  db:
    image: postgres:latest
    container_name: pg_container
    restart: always
    environment:
      POSTGRES_PASSWORD: root
      POSTGRES_USER: root
      POSTGRES_DB: testdb
    ports:
      - '5432:5432'
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - db_network

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin4_container
    restart: always
    ports:
      - '8888:80'
    environment:
      PGADMIN_DEFAULT_EMAIL: pgadmin@example.com
      PGADMIN_DEFAULT_PASSWORD: root
    networks:
      - db_network

volumes:
  pgdata:

networks:
  db_network:

```

Explanation

In this configuration file, we define two services: db and pgadmin. The db service is responsible for running the PostgreSQL instance, while the pgadmin service is responsible for running the pgAdmin web interface.

The db service uses the postgres image from the Docker Hub registry. We specify the volume mapping to store the data files in the local_pgdata volume. The ports section maps the container port 5432 to the host port 5432, allowing you to access the PostgreSQL instance from your local machine.

We also set the environment variables `POSTGRES_DB`, `POSTGRES_USER`, and `POSTGRES_PASSWORD` to configure the database name, username, and password, respectively.

The pgadmin service uses the dpage/pgadmin4 image from the Docker Hub registry. We map the container port 80 to the host port 8888 to access the pgAdmin web interface.
Starting PostgreSQL

Now that you have created the docker-compose.yml file, you can start the PostgreSQL container by running the following command in the terminal:

```

docker-compose up -d

```
This command will download the necessary images and start the PostgreSQL and pgAdmin containers in the background. You can verify that the containers are running by executing the following command:

```

docker ps

```

This command will display a list of running containers on your system. You should see the db and pgadmin containers listed in the output.
Accessing pgAdmin

You can now access the pgAdmin web interface by opening a web browser and navigating to http://localhost:8888. In the login page, enter the email pgadmin@example.com and password root that you specified in the docker-compose.yml file. You should now be able to interact with your PostgreSQL database through the pgAdmin web interface.
Database Connection URL

If you want to connect with a database URL, you can use the following URL:

```

postgresql://root:root@localhost:5432/testdb

```

That's it! You have successfully set up PostgreSQL using Docker on your system. You can now start developing applications that use PostgreSQL as the backend database.
