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
