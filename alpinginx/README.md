## Minimal Docker image for Nginx on Alpine Linux.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ![nginx-logo](https://cloud.githubusercontent.com/assets/604609/11711944/ea8bb374-9f21-11e5-84b9-ae71b6e75990.jpg) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
![alpinelinux-logo](https://cloud.githubusercontent.com/assets/604609/11691594/a255c628-9e93-11e5-8a0b-3275b8437c98.jpg)

For anyone who wishes to use this image for their own container projects - note that I shall endeavor to keep it tracking the latest release of [Nginx](https://www.nginx.com) and [Alpine](http://www.alpinelinux.org/).

---

### Specs 

Docker Tag     |    Versions                       |   Description             |  Size (compressed)
---------------|-----------------------------------|---------------------------|--------------------------
`latest`       |  Nginx `1.9.7`<br>Alpine `3.2.3`  | Plain install of Nginx    | 26 mb (10 mb)      

---

### Configuration + Ports

The image exposes ports:   `80`  `443`

The image sets up the Nginx document root for the default virtual host at `/app/nginx`.

Path                     |        Resource
-------------------------|---------------------------
`/app/nginx`             |  Default document root
`/usr/sbin/nginx/`       |  Nginx Executable    
`/etc/nginx/`	         |  Configuration path    
`/var/log/nginx/`	     |  Logs    
`/tmp`		             |  PID    


---

### Usage 

After executing the following - and assuming port 80 was free on your host - you should be able to view the default Nginx welcome page at the IP of your host. 

```bash
docker run -d -p 80:80 jonjack/alpinginx
```

---

### Using as a HTTP Server

Assuming you are using Nginx as a HTTP Server (not just as a reverese proxy), one option for updating your site's content is to mount a data volume in the path of your Nginx document root. This way you can then easily push your content updates into the mounted path on the host. 

The default document root is set at `/app/nginx` in the container. If we start a container as follows you can then push your content changes into `/host/path/nginx/html` on the host machine - these changes should then get reflected by Nginx running in the container.

```bash
docker run -d -p 80:80 -v /host/path/nginx/html:/app/nginx jonjack/alpinginx
```

---

### Why Another Image?

There are a few Nginx on Alpine images already, but I had some specific use case of my own:-

- verifies the integrity of the Nginx archive as per the best practises for the official images
- uses latest version of Nginx
- Nginx docroot at `/app/nginx`
- Removes any unnecessary leftovers of the build

