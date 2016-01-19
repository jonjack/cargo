## Docker image for running Typesafe's Activator.

![typesafe-activator](https://cloud.githubusercontent.com/assets/604609/12071125/859e47b0-b092-11e5-99a0-e530a20917b1.png) &nbsp;&nbsp;&nbsp;&nbsp; 
![scala-logo](https://cloud.githubusercontent.com/assets/604609/12071130/b4662b9e-b092-11e5-8705-d7946eb52322.png)

---

This image is intended for local development using Typesafe's [Activator](http://www.typesafe.com/activator/download) platform.

Base image: [jalpine:jdk](https://hub.docker.com/r/jonjack/jalpine/) (Oracle JDK running on Alpine Linux).

---

### Technology Stack

```bash
+------------------------+
|       Activator        |
|   Play, Scala, Akka    |
+------------------------+
|     Oracle JDK 1.8     |
+------------------------+
|      Alpine Linux      |
+------------------------+
|         Docker         |
+------------------------+
```

---

### Configuration + Ports

The image exposes the following ports:   

`80` `443` (from base image - [jalpine:jdk](https://hub.docker.com/r/jonjack/jalpine/))    
`9000` (default Netty HTTP server port)

---

### Setup

The default (`latest`) tag for this image installs the Typesafe [Activator](http://www.typesafe.com/activator/download) minimal package which contains no dependencies. This means that when you run any `activator` commands for the first time you will need to wait for some time (depending on your network bandwidth) while Activator updates the local Ivy cache with all the required dependencies. This should be a one-time task for each container you setup based off of this image.

#### Why not use the full Activator package?

An alternative would have been to install the full Activator package within the image but this ships with around 500mb of cached libraries, many of which you may not need. 

If you create a container from this image and then create a barebones project - using the Play-Scala template for example - then Activator will pull down around 120mb of dependencies. Depending on how much of Typesafe's reactive stack you wish to use, its better to keep the Docker image lightweight by just providing the minimal Activator package which you can then build on for whatever your needs. Just remember that the first time you run activator commands your build will take a hit as the required dependencies are pulled down and cached.

#### Create your own image with a populated cache

If you need to create multiple containers using this image (maybe a whole team decide to use it locally) then you could create your own image after populating the Ivy cache.


```bash
# in the Docker CLI, pull the image
$ docker pull jonjack/activator

# run a container
$ docker run -it jonjack/activator /bin/sh
# now inside the container, run activator & wait a while while the ivy cache gets populated
$ activator

Getting org.scala-sbt sbt 0.13.8 ...
downloading https://repo.typesafe.com/typesafe/ivy-releases/org.scala-sbt/sbt/0.13.8/jars/sbt.jar ...
	[SUCCESSFUL ] org.scala-sbt#sbt;0.13.8!sbt.jar (2936ms)
...
# exit the container
$ exit

# check the container ID
$ docker ps -a
CONTAINER ID     IMAGE           COMMAND       CREATED       STATUS 
75c7fa155037     ff021bb4e523    "/bin/sh"     4 hours ago   Exited 4 mins ago

# commit the updated container to a new image
$ docker commit -m "Populated Ivy cache" -a "Joe Bloggs" 75c7fa155037 yourorg/activator:v2
82a130884e007b097a7982b125e5a5b56b8a6c51c91aaf365dc724b9e91950ea

# now you can see your version of the image with the size to reflect the updated cache
$ docker images
REPOSITORY            TAG       IMAGE ID         CREATED          VIRTUAL SIZE
yourorg/activator     v2        82a130884e00     A minute ago     400.9 MB
activator             latest    ff021bb4e523     4 hours ago      171.8 MB

# now you can use your own image for your Activator containers
$ docker run -it yourorg/activator:v2 /bin/sh
```

To run the container in detached mode pass your application start script as the command.

```bash
docker run -d -v /host/application:/app yourorg/activator:v2 /app/start-script
```


