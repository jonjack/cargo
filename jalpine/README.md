## Minimal Docker image for Java on Alpine Linux.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![java-bean](https://cloud.githubusercontent.com/assets/604609/11711952/ffaa4b3a-9f21-11e5-9cd6-e3cb705c2146.jpg) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
![alpinelinux-logo](https://cloud.githubusercontent.com/assets/604609/11691594/a255c628-9e93-11e5-8a0b-3275b8437c98.jpg)

---

The default image (`latest`) provides is intended for production and testing environments since it only provides the Server JRE. If you want to use this for development then use the `jdk` tag.

For anyone who wishes to use this image for their own container projects note that I shall endeavor to keep it tracking the latest release of [Java](https://www.oracle.com/java/index.html) and [Alpine](http://www.alpinelinux.org/).

---

### Specs 

Docker Tag    |  Size (compressed)  |  Versions                               |  Description
--------------|---------------------|-----------------------------------------|-------------------------
`latest`      | 124 mb (48 mb)      | Java `1.8.0_72_b15` <br>Alpine `3.3.1`  | 64 bit Server JRE
`jdk`         | 165 mb (62 mb)      | Java `1.8.0_72_b15` <br>Alpine `3.3.1`  | 64 bit JDK

---

### Configuration + Ports

The image exposes the following ports:   `80`  `443`

---

### Usage 

The Java Virtual Machine needs some code to execute to start a process so you have a couple of options for using this image:-

1. Either use it as a base image for your own

 ```bash
FROM jonjack/jalpine

EXPOSE [any other ports you need]
CMD [some command to run]
ENTRYPOINT [your entrypoint]
```

2. Place your Java application on the host somewhere and mount this pth as a volume into your container.    

 Assuming you intend to bootstrap you application with a class called `Main` in the host path `/host/app/path`, you could start up the container and the application like so:

 ```bash
docker pull jonjack/jalpine

docker run -d -v /host/app/path:/app/path 
                             jonjack/jalpine java -cp /app/path Main
```

If you want to use the JDK instead ie. for local development purposes, then use the `jdk` tag

```bash
docker pull jonjack/jalpine:jdk
```


