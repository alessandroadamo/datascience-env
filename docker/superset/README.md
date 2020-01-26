Superset Visualization Tool
===========================


Build the Image
---------------

To build the image is required to run the following code in the shell

```console
foo@bar:~$ docker build -t superset -f .\Dockerfile-superset .
```

Run the Service
---------------

To run the service execute the following script

```console
foo@bar:~$ docker run --rm -d --name superset1 -p 8088:8088 -v [persistent db path]:/home/superset/.superset superset
```

First Run Initialization
------------------------

At the first run of the container is required to connect to the container 

```console
foo@bar:~$ docker exec -it superset1 /bin/bash
```

and initialize the database used by Superset.

```console
foo@bar:~$ flask fab create-admin --username superset --firstname superset --lastname superset --email superset --password superset
foo@bar:~$ superset db upgrade
foo@bar:~$ superset init
foo@bar:~$ superset load_examples
```