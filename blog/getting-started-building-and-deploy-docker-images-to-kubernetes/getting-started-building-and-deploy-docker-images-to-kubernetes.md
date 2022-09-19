In this tutorial, we are gonna build and deploy docker images to Kubernetes from scratch.

What are docker and Kubernetes?

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production. ([Docker](https://docker.com))

[Kubernetes](https://kubernetes.io/docs/concepts/overview/), also known as K8s, is an open-source system for automating the deployment, scaling, and management of containerized applications.

It groups containers that make up an application into logical units for easy management and discovery. ([Kubernetes](htts://kubernetes.com))

Before getting started that, we must make sure we have docker and Kubernetes Installed on the machine. You can see docker installation instructions on this page: https://docs.docker.com/engine/install/, and for Kubernetes, you can use Minikube https://minikube.sigs.k8s.io/docs/start/, Kind https://kind.sigs.k8s.io. or if you use docker desktop you can install Kubernetes inside that.

In this tutorial we do not explain much detail about the installation, you can check the URL on the top.

Okay if all the requirements are finished, we can get started now. for building and deploy, I divide it into three parts or steps, which consist of the following:


1. **Build Docker image**
<br>
   In this step, we will build our image from scratch. First prepare the application you goin to use to build inside the docker image, in this tutorial I am going to write a simple application using the go/golang programming language.

```go
package main

import (
	"flag"
	"fmt"
	"log"
	"net/http"
	"os"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
	hostname, err := os.Hostname()
	if err != nil {
		http.Error(w, "server error", http.StatusInternalServerError)
		return
	}
	_, err = fmt.Fprintf(w, "Hello from host %s", hostname)
	if err != nil {
		http.Error(w, "server error", http.StatusInternalServerError)
		return
	}

}

func main() {

	port := flag.Int("port", 8080, "-port and then server port")

	flag.Parse()

	mux := http.NewServeMux()
	mux.HandleFunc("/", helloHandler)

	srv := &http.Server{
		Addr:    fmt.Sprintf("0.0.0.0:%d", *port),
		Handler: mux,
	}

	log.Printf("Server running on port: %d\n", *port)
	if err := srv.ListenAndServe(); err != nil {
		log.Println(err)
		os.Exit(1)
	}
}
```

After we create our server, now we create a Dockefile for initialized docker image

```dockerfile
# Build stage
FROM golang:1.19-alpine3.16 AS builder
ARG SOURCE_LOCATION=/app
WORKDIR ${SOURCE_LOCATION}
ADD go.mod go.mod
COPY . .
ENV GO111MODULE on
RUN go mod download
RUN go build -o app main.go

# Run stage
FROM alpine:3.16
ARG BUILDER_SOURCE=/app
LABEL maintainer="Ludin Nento <ludyyn@gmail.com>"
WORKDIR ${BUILDER_SOURCE}
COPY --from=builder ${BUILDER_SOURCE}/app .
```

You can see in this Dockerfile, that we are using a multi-stage build. according to the docker website “Multistage builds are useful to anyone who has struggled to optimize Dockerfiles while keeping them easy to read and maintain.”

After finish creates a Dockerfile, then run the following command to build a docker image : 
```shell
docker build -t DOCKER_IMAGE_NAME .
```

if you are not inside the docker file location, you can run the following command :

```
docker build -t DOCKER_IMAGE_NAME -f DOCKER_FILE_PATH/Dockerfile .
```

The DOCKER_IMAGE_NAME is up to you. you can name the image that you want. in my case, I will name the name demo.

After the build process is done, you can check the image by running the command
```shell
docker images
```
or
```shell
docker image ls
```

And you will see all images that you have, and the image that you build before


2. **Upload the image**
<br>
   Before you push an image you must check the image your build exits or not, with the command docker images or docker image ls

```shell
docker images
```
or
```shell
docker image ls
```

After that, you must log in to your docker hub, with your docker hub account. if you do not have an account on docker hub you can create one on this page https://hub.docker.com.

After creating an account. you must run the command :
```shell
docker login
```

The docker login command is used to log in to our docker account, before pushing our docker image to the remote repository

Next, you must set your docker image with a tag. I will create a tag for my image with 
```shell
ludinnento/demo:latest
```
**luddinnento** is my docker account, and demo is the docker image name, last is the version, I set my tag version to the latest.

```shell
DOCKER_USERNAME/TARTGET_NAME:VERSION
```

To make a docker image tag you must run the following command:
```shell
docker tag demo ludinnento/demo:latest
```

After that, we are gonna push the image on the docker hub. To push the image you must run the following command:
```shell
docker push ludinnento/demo:latest
```

**docker push** command is used to upload our docker image to the registry or remote docker repository

After that, you can check your docker hub if the image that you push or upload is exits


3. **Deploy Image To Kubernetes**
<br>
   To deploy the application to Kubernetes, first, make sure you already install Kubernetes on your computer or you can use Kubernetes on cloud services, like Google Cloud Platform, Amazon Web Service, and Azure. And don’t forget to install kubectl, for communicating/controlling the Kubernetes cluster. 

    The first command that we want to run is the kubectl version, this command is used to check the Kubernetes version.

    ```shell 
    kubectl version
   ```

   After that run kubectl get nodes, the command to check Kubernetes cluster node.

    ```shell
    kubectl get nodes
   ```

   In this step, we are gonna deploy Kubernetes with minimal configuration, and we create Kubernetes deployment.yaml, and service.yaml. 

   Kubernetes Deployment is the process of providing declarative updates to Pods and ReplicaSets. It allows us to declare the desired state in the manifest file or YAML file. ([Kubernetes](https://kubernetes.io))

   Kubernetes Service is Service is an abstraction that defines a logical set of Pods and a policy by which to access them (sometimes this pattern is called a micro-service). The set of Pods targeted by a Service is usually determined by a selector. ([Kubernetes](https://kubernetes.io))

   The following is an example of a Deployment, that we are using in this tutorial


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo
  labels:
    app: demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
    spec:
      containers:
        - name: demo
          image: ludinnento/demo:latest
          ports:
            - containerPort: 8080
```


Before you begin, make sure your Kubernetes cluster is up and running. Follow the steps given below to create the above Deployment:

1. Create the Deployment by running the following command:
```shell
kubectl apply --namespace demo -f hack/k8s/deployment.yaml
```
2. Run **kubectl get deployment** to check if the Deployment was created.
```shell
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
demo   1/1     1            1           3m33s
```

When you inspect the Deployments in your cluster, the following fields are displayed:

- `NAME` lists the names of the Deployments in the namespace.
- `READY` displays how many replicas of the application are available to your users. It follows the pattern ready/desired.
- `UP-TO-DATE` displays the number of replicas that have been updated to achieve the desired state.
- `AVAILABLE` displays how many replicas of the application are available to your users.
- `AGE` displays the amount of time that the application has been running.


3. After that we create service.yaml :
```yaml
apiVersion: v1
kind: Service
metadata:
  name: demo
  labels:
    app: demo
spec:
  ports:
    - port: 8080
      protocol: TCP
      targetPort: 8080
  selector:
    app: demo
  type: ClusterIP
```

You can see that it looks somewhat similar to the Deployment resource we showed/create earlier. however, the kind is service.

4. Run **kubectl apply -f hack/k8s/service.yaml** : if successful it will return
```shell
service/demo created
```

5. Run **kubectl get services** to show the service that we created before. It will get results like the following
```shell
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
demo         ClusterIP   10.103.121.111   <none>        8080/TCP   72s
```

If you want to try to access the application in the browser, the application cannot be accessed because the external IP has not been set. to make the application accessible, we have to port the application.

6. Run **kubectl port-forward service/demo 9999:8080**, it will connect the demo service to a port on your local machine.
```shell
Forwarding from 127.0.0.1:9999 -> 8080
Forwarding from [::1]:9999 -> 8080
Handling connection for 9999
```

7. Last, run **kubectl delete -f hack/k8s/** to clear all resources that we created before.
```shell
deployment.apps "demo" deleted
service "demo" deleted
```

That is all and thank you. if you are interested you can see the source code on my [Github Repository](https://github.com/fn-code/withfun/tree/master/docker-example)