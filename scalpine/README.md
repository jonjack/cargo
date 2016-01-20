# scalpine

Docker image for [Scala](http://www.scala-lang.org/) on [Alpine](http://www.alpinelinux.org/) Linux.

Scala version: `2.11.7`    
Current size: `150 MB`

Based on [jonjack/jalpine](https://hub.docker.com/r/jonjack/jalpine/) - minimal image for Java 8 Server JRE on Alpine Linux.

---

### Usage

```bash
docker pull jonjack/scalpine
```

Test a container.

```bash
docker run -it jonjack/scalpine scala -version
```
