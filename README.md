# nodejs-tester-server
This repository showcases how to create a container image with a Nodejs Hello World



## How to

```
podman build -t node-app .
podman run localhost/node-app
podman run --env PORT=8080 localhost/node-app
```
