# nodejs-tester-server
This repository showcases how to create a container image with a Nodejs Hello World.

The code is based on the following repository from the Red Hat Software Collections: https://github.com/sclorg/s2i-nodejs-container/blob/master/12/README.md 


## 1. How to deploy app on OCP 

```
oc new-app nodejs:14~https://github.com/alvarolop/nodejs-tester-server
```

Now, substitute the configuration of the deployment with the configuration of the file `deployment.yaml`:

* Sidecar annotation.
* Liveness and readiness probes.
* Injecting the variable HOST using the pod name. This is the configuration that breaks the probes.


## 2. How to deploy app on OCP manually

```
oc new-app nodejs:14~https://github.com/alvarolop/nodejs-tester-server
```

After creating the application, you may need to do the following:

```bash
# Include the istio annotation
oc patch deployment nodejs-tester-server --type='json' -p "[{\"op\": \"add\", \"path\": \"/spec/template/metadata/annotations\", \"value\": {\"sidecar.istio.io/inject\": \"true\"}}]"

# Add an environment variable to listen on the pod name.

# Add liveness and readiness probes.

```


## 3. How to create image in local

```bash
podman build -t node-app .
podman run localhost/node-app
podman run --env PORT=8080 localhost/node-app
```
