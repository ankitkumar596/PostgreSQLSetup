Introduction

PostgreSQL is a powerful, open-source object-relational database system. It is a highly scalable, SQL-compliant database management system that is used to handle large workloads. PostgreSQL is a popular choice for many developers and organizations due to its robust features, extensibility, and reliability.

In this tutorial, we will walk you through the process of setting up PostgreSQL on your system. In this modern age, you can take advantage of Docker to easily set up and run PostgreSQL on your local machine. Docker is a platform that allows you to package, distribute, and run applications in containers. It provides a lightweight and efficient way to run applications in isolated environments. Docker is available for Windows, macOS, and Linux, making it a versatile tool for developers.
Prerequisites

Before you begin, you will need to have the following prerequisites:

    A system running Windows, macOS, or Linux

    Docker installed on your system

    Basic knowledge of using the command line

Once the docker is installed, you can verify the installation by running the following command in your terminal:
``` docker --version ```

This command will display the version of Docker installed on your system.

Now that you have Docker installed, create a new directory for your PostgreSQL data. This directory will be used to store the data files for your PostgreSQL instance. I usually keep this directory in my project folder so that it is easy to manage.

Then, create a new file named docker-compose.yml in the same directory. This file will contain the configuration for your PostgreSQL container.

Insert the following content into the docker-compose.yml file:

```
version: '3'
services:
  db:
    image: postgres
    restart: always
    volumes:
      - ./data/db:/var/lib/postgresql/data
    ports:
      - 5432:5432  # make sure you don't have another container running on 5432

    environment:
      - POSTGRES_DB=chaiDB
      - POSTGRES_USER=chaiaurcode
      - POSTGRES_PASSWORD=chaiaurcode

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080
  ```

In this configuration file, we define two services: db and adminer. The db service is responsible for running the PostgreSQL instance, while the adminer service is responsible for running the Adminer web interface. Adminer is a lightweight database management tool that allows you to interact with your databases through a web interface.

The db service uses the postgres image from the Docker Hub registry. We specify the volume mapping to store the data files in the ./data/db directory. The ports section maps the container port 5432 to the host port 5432, allowing you to access the PostgreSQL instance from your local machine.

We also set the environment variables POSTGRES_DB, POSTGRES_USER, and POSTGRES_PASSWORD to configure the database name, username, and password, respectively.

The adminer service uses the adminer image from the Docker Hub registry. We map the container port 8080 to the host port 8080 to access the Adminer web interface.

Now that you have created the docker-compose.yml file, you can start the PostgreSQL container by running the following command in the terminal:

```
docker-compose up -d

```

This command will download the necessary images and start the PostgreSQL and Adminer containers in the background. You can verify that the containers are running by executing the following command:

```

docker ps

```

This command will display a list of running containers on your system. You should see the db and adminer containers listed in the output.

You can now access the Adminer web interface by opening a web browser and navigating to http://localhost:8080. In the login page, enter the database name, username, and password that you specified in the docker-compose.yml file. You should now be able to interact with your PostgreSQL database through the Adminer web interface.

If you want to connect with database url, you can use the following url:

```

postgresql://chaiaurcode:chaiaurcode@localhost:5432/chaiDB

```

That's it! You have successfully set up PostgreSQL using Docker on your system. You can now start developing applications that use PostgreSQL as the backend database.
