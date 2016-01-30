## Minimal container for running a Typesafe [Play](https://www.playframework.com/) application.

Base image: [jalpine](https://hub.docker.com/r/jonjack/jalpine/).    
See Typesafe's [Play](https://www.playframework.com/) website if you are not familiar with the framework.

---

### Technology Stack

The image is *minimal* since it uses [jalpine](https://hub.docker.com/r/jonjack/jalpine/) as its base image which is a trimmed down Oracle 8 Server JRE running on Alpine Linux. The container is around 124 Mb in size (before your Play application and its dependencies have been added).

```bash
+------------------------+
|          Play          |
+------------------------+
|  Oracle Server JRE 8   |
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

The image assumes a startup script for your Play application at `/app/play/bin/start`. It also assumes you are using Play's default Netty port of `9000`.

If you use the image as is, then you can start the container (and your Play application) like this.

```bash
docker run -d -p 80:9000 play
```

If you have your application files on the host and wish to mount them into the container then you can do something like this.

```bash
docker run -d -p 80:9000 -v /app/play:/app/play play
```
