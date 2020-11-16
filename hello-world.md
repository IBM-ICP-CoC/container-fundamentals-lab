
# Hello World

1. In a terminal window on your local machine with Docker installed, run the dockr command to verify that there are no container images stored locally (it is OK if there are, that just means you or someone else has been using Docker locally).

```shell
docker images
```
The output will probably look something like the following:

```shell
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

2. Use the Docker `run` command to both pull and run the standard hello world container.

```shell
docker run hello-world
```

The output will look something like the following:
```shell
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

3. Now list the container images again.

```shell
docker images
```

You should see an image in the list from the Repository `hello-world`.  This image was pulled and stored locally so that the container could run and display the output you saw.

4. List the containers on your workstation with:
```shell
docker ps -a
```

The oputput will look something like the following:
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS                  NAMES
2be3e5c6573f        hello-world         "/hello"                 2 minutes ago       Exited (0) 2 minutes ago                          musing_curran
```

This indicates that a contain was run, and that it exited without error, given the value 0.

5. You can remove this exited container with the `docker rm` command and passing in the name of the container (i.e. `musing_curran`) or the container ID (i.e. `2be3e5c6573f`).  

Remove your containerusing either your container id 
```shell
docker rm 2be3e5c6573f
```
or the container name.
```shell
docker rm musing_curran
```

----

[Back to Overview](README.md)