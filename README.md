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

| Parameter      |  Value       | 
| -------------- |:------------:| 
| System         | PostgresSQL  | 
| Server         | postgresql   | 
| Username       | postgresql   | 
| Password       | postgresql   | 
| Database       | postgresql   | 

# Upload an Object to Minio from Jupyter

From Jupyter is possible to store and retrive binary objects stored on Minio repository.
To do this, is required to create a minio client.

```python
import pickle
import minio
from minio.error import ResponseError

endpoint="datascience-minio:9000"
minio_access_key="minio"
minio_secret_key="minio123!"

bytes_dump = pickle.dumps(model) 

minioClient = minio.Minio(endpoint = endpoint, 
                          access_key = minio_access_key, 
                          secret_key = minio_secret_key,
                          secure=False
                         )
```

To store an object into a Minio bucket use the method *put_object* of the Minio client as follow.
```python
bucket_name="models"
object_name="model-" + datetime.datetime.utcnow().isoformat()

minioClient.put_object(bucket_name=bucket_name,
                       object_name=object_name,
                       data=io.BytesIO(bytes_dump),
                       length=len(bytes_dump)
                      )
```

If the bucket does not exist, to create it execute the following code.

```python
minioClient.make_bucket(bucket_name)
```

To retrive a previously stored model object is required to execute the *get_object me* method of the client and deserialize the object with the pickle *load* function.

```python
model = pickle.loads(minioClient.get_object(bucket_name=bucket_name,
                                       object_name=object_name
                                      ).read()
                    )
```
