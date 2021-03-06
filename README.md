# cargo

Playing around with Docker image creation.

---

Most of these images are based on top of Alpine Linux to follow the pratice of making images as small and lightweight as possible. These images are generally built for my own needs but most should be available in the [public repository](https://hub.docker.com/u/jonjack/) in case anyone else finds them useful. 

---

### Alpinginx

Nginx HTTP server.


### Alpinjet

Java + Jetty on Alpine. This provides the out of the box Jetty implementation.


### Alpinode

Node + NPM.


### Alpivator

Intended for local development using Typesafe's [Activator](http://www.typesafe.com/activator/download) platform.


### Jalpine

Java running on Alpine.

This image provides tags for both the 64 bit Server JRE and the JDK versions depending on your needs.


### Redpine

Redis memory key:value store on Alpine.



### Scalpine

Scala running on Alpine. This image is intended for development environments since you would normally deploy the Scala libraries as application dependencies.


### Yalp

Java Server JRE (jalpine) configured to start a Typesafe Play application.

This image is not currently in the public repository so if you wish to use it you will need to clone the repo and build the image.

Assuming you are in a Docker CLI (and have Git installed):

```bash
git clone https://github.com/jonjack/cargo.git

cd yalp

docker build -t yalp .
```


