# docker-alpinode

Docker image which includes Node.js on Alpine Linux.

- [Alpine](http://www.alpinelinux.org/) - small footprint Linux    
- [Node](https://nodejs.org) - non-blocking event-driven Javascript runtime

---

### Usage

You can get the image in one of two ways.

#### 1. Build it yourself

Build from the Dockerfile (will take a few minutes while node is built from source for Alpine).

```bash
docker build -t alpinode github.com/jonjack/docker-alpinode
```

#### 2. Import a Release

Grab a [release](https://github.com/jonjack/docker-alpinode/releases) and then import.  


```bash
docker import alpinode.tar alpinode
```

Check the image.

```bash
docker images

REPOSITORY     TAG         IMAGE ID          CREATED             VIRTUAL SIZE
alpinode       latest      31daff05cc61      35 minutes ago      35.27 MB
```

---

### Run a container

The following example maps port 80 and sets up a volume.

```bash
docker run -it --name alpinode -p 80:80 -v /apps/node:/app alpinode /bin/sh
```

Maps the host port `80` to the container port `80`.       
Mounts the host directory `/apps/node` into the container volume at `/app` - now we can push our Node scripts onto the host at `/apps/node` and they will be available in the container at `/app`.

---

### Ports

Note that the Dockerfile exposes `80`, `8080` so you can map to any of these when you run a container. If you have other requirements then fork my repo and amend the Dockerfile to suit your needs.

---

### npm Dependencies

If you have `require()`ments in your node scripts then you will need to install them into `/app/node_modules` or `/path/to/your/node/scripts/node_modules`.

Example. 

```bash
docker exec -it CONTAINER_ID /bin/sh

cd /app

npm install restful
```

---

### Hello World

Start a container, mapping port `8080` and mounting a volume.

```bash
$ docker run -it -p 8080:8080 -v /apps/node:/app alpinode /bin/sh
```

Install [restful](https://www.npmjs.com/package/restful) Node module.

```bash
$ cd /app 
$ npm install restful
```

Now drop this script into `/apps/node` on your host calling it `server.js` or something.

```javascript
  var http = require('http'),
      director = require('director');

  function helloWorld() {
    this.res.writeHead(200, { 'Content-Type': 'text/plain' })
    this.res.end('Hello from Nodejs!');
  }

  var router = new director.http.Router({
    '/hello': {
      get: helloWorld
    }
  });

  var server = http.createServer(function (req, res) {
    router.dispatch(req, res, function (err) {
      if (err) {
        res.writeHead(404);
        res.end();
      }
    });
  });

  server.listen(8080);
```

Back in the container, run the server script.

```bash
node server.js
```

Now you should be able to visit [192.168.99.100:8080/hello](http://192.168.99.100:8080/hello)

If you do not see "Hello from Nodejs" in your browser then first check the IP address of the running container with:

```bash
docker inspect --format '{{ .NetworkSettings.IPAddress }}' CONTAINER_ID
```

---

### Guidelines

- the PATH on Alpine is `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`
- Node is a program so goes in `/usr/bin` (already in PATH)
- NPM is a library I guess so goes in `/usr/lib/node_modules/npm/bin/`. It also has sym link in `/usr/bin` so we can call it on the command line (since `/usr/bin` already in PATH))
- `npm install MODULE -g` shoves it into `/usr/lib/node_modules`. But we will want to use NPM modules in our applications using `require` most probably so any NPM modules that we `require` in our Node scripts should live in `/path/to/app/node/scripts/node_modules`.  Use `npm install -g` when you want to use the module on the commnd line (rather tha using `require`)
- [npm guidelines](https://docs.npmjs.com/files/folders)



