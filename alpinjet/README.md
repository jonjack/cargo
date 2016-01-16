## Minimal Docker image for Jetty 0N Java 8 Server JRE on Alpine Linux.

#### Build an Image

```bash
docker build -t alpinjet - < Dockerfile
```

#### Run the Container

The Dockerfile exposes Jetty's default port `8080`.   
The following maps the host's port 80 to the container's exposed port. If you wish to map a different host port then use `-p [your port]:8080`.

```bash
docker run -d -p 80:8080 alpinjet
```

You should now be able to access the Jetty base demo page at [http://[container IP]](http://0.0.0.0).

If you mapped a different port, say `-p 8080:8080`, then you need to use [http://[container IP]:8080](http://0.0.0.0:8080)

---

#### Getting Your VM's IP

Assuming your machine is `default` you can get the continer IP address with:

```bash
$ docker-machine ip default

192.168.99.100
```

If you have multiple machines running on your host then use:

```bash
$ docker-machine ls

NAME      ACTIVE   DRIVER       STATE     URL                         SWARM
default   *        virtualbox   Running   tcp://192.168.99.100:2376
dev       *        virtualbox   Running   tcp://192.168.99.101:2376
```