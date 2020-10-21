# nodejs-tester-server
This repository showcases how to create a container image with a Nodejs Hello World


## How to deploy app on OCP 

```
oc new-app nodejs:14~https://github.com/alvarolop/nodejs-tester-server
```

After creating the application, you may need to do the following:

```bash
# Include the istio annotation
oc patch deployment nodejs-tester-server --type='json' -p "[{\"op\": \"add\", \"path\": \"/spec/template/metadata/annotations\", \"value\": {\"sidecar.istio.io/inject\": \"true\"}}]"

# 


```


## How to create image in local

```bash
podman build -t node-app .
podman run localhost/node-app
podman run --env PORT=8080 localhost/node-app
```
