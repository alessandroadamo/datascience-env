# Datascience Docker Environment

Full web based **datascience environment**. This environment is implemented as a **docker-compose** configuration file.
It is thinked to be a full customizable datascience environment containing databases, visualization tools and a model storage system.

## Features
- [Jupyter](https://jupyter.org/) interactive development environment
- [PostgreSQL](https://www.postgresql.org/) relational database
- [Minio](https://min.io/) object storage
- [Adminer](https://www.adminer.org/) database management
- [Superset](https://superset.incubator.apache.org/) business intelligence web application
- [Redis](https://redis.io/) non-relational database
- [RedisInsight](https://redislabs.com/blog/redisinsight-gui/) GUI for Redis
- [MongoDB](https://www.mongodb.com/) non-relational database
- [Mongo Express](https://github.com/mongo-express/mongo-express) MongoDB management tool

# Install and Run
To start the environment it is required to clone the repository and execute the **docker-compose** command, and after a coucle of coffea you will have a full up and running datascience environment.
``` 
foo@bar:~$ git clone https://github.com/alessandroadamo/datascience-env
foo@bar:~$ cd datascience-env
foo@bar:~$ docker-compose up
```
To access to the different tools, open a web browser and navigate to *localhost*.
In the following table are listed all the services on the default ports.

| Service        | Link                                              | 
| -------------- |:-------------------------------------------------:| 
| Jupyter        | [http://localhost:8888/](http://localhost:8888/)  | 
| Superset       | [http://localhost:8088/](http://localhost:8088/)  | 
| Adminer        | [http://localhost:8080/](http://localhost:8080/)  | 
| RedisInsight   | [http://localhost:8001/](http://localhost:8001/)  | 
| MongoExpress   | [http://localhost:8081/](http://localhost:8081/)  | 
| Minio          | [http://localhost:9000/](http://localhost:9000/)  | 

# Connect to PostgreSQL from Adminer
To create a connection to postgresql docker container from Adminer service, from the page [http://localhost:8080/](http://localhost:8080/) create a new connection with the following pamaters:
```
| Parameter      |  Value       | 
| -------------- |:------------:| 
| System         | PostgresSQL  | 
| Server         | postgresql   | 
| Username       | postgresql   | 
| Password       | postgresql   | 
| Database       | postgresql   | 
```

![alt text](https://github.com/alessandroadamo/datascience-env/blob/master/img/adminer_postgres.PNG "Adminer connection creator")
