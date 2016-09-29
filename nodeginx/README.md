# docker-nodeginx

Docker composition of Nginx backed by Node.

Sample Docker `compose` example of running 2 containers with Nginx as a HTTP Server for serving static content and Node for providing a business tier so to speak - albeit just in another Docker container. The idea is to provide a Docker blueprint for getting small simple website platforms up and running quickly and efficiently.

- [Nginx](https://www.nginx.com) - high-performance, non-blocking, event-driven HTTP Server to manage the static content 
- [Node](https://nodejs.org) - high-performance, non-blocking, event-driven Javascript runtime for managing the dynamic content
