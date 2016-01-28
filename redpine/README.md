
## Minimal Docker image for Redis on Alpine Linux

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![redis-logo](https://cloud.githubusercontent.com/assets/604609/12272916/c4c567ea-b95a-11e5-8bf7-4ce0d2078ae9.png)

---

### Specs 

Docker Tag    |  Size (compressed)  |  Versions                           |  Description
--------------|---------------------|-------------------------------------|-------------------------
`latest`      | 12 mb (5 mb)        | Redis `3.0.5` <br>Alpine `3.3.3`    | Redis Server + Tools

---

### Configuration + Ports

The image exposes the following ports:   

`6379` - default server port    
`16379` - clustering support    
`26379` - Sentinal support    

---

### Usage 

Get the image from the public repository.

```bash
docker pull jonjack/redpine
```

Run the container with the defaults and minimal setup.

```bash
docker run -d redis redis-server
```

Give it a name maybe.

```bash
docker run -d --name redis redis redis-server
```

You can provide a custom configuration file by installing on the host machine somewhere and mounting this as a volume inside the container. You then pass the `/container/path/redis.conf` path as a parameter to the `redis-server` command.

```bash
docker run -d --name redis -v /host/path:/container/path 
                    redis redis-server /container/path/redis.conf
```




