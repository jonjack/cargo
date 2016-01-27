# cargo

My collection of Docker images.

---

Most of these images are based on top of Alpine Linux since I like the pratice of making images as small and lightweight as possible. These images are generally built for my own needs but they are available in the [public repository](https://hub.docker.com/u/jonjack/) in case anyone else finds them useful. 

---

### Alpinginx

Nginx HTTP server.

```bash
docker pull jonjack/alpinginx
```

### Alpinjet

Java + Jetty on Alpine. This provides the out of the box Jetty implementation.


### Alpinode

Node + NPM.


### Alpivator

Intended for local development using Typesafe's [Activator](http://www.typesafe.com/activator/download) platform.


### Jalpine

Java running on Alpine.

This image provides tags for both the 64 bit Server JRE and the JDK versions depending on your needs.

For 64 bit Server JRE, do a:

```bash
docker pull jonjack/alpinginx
```

For JDK, do a:

```bash
docker pull jonjack/alpinginx:jdk
```

### Redpine

Redis memory key:value store on Alpine.


### Scalpine

Scala running on Alpine. This image is intended for development environments since you would normally deploy the Scala libraries as application dependencies.
