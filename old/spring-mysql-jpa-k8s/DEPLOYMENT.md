# Simple generator for Kubernetes resources

This generator creates a Kubernetes Service and Deployment Resource to deploy a Spring Boot application.  It also can create the Kubernetes resources for deploying a MySQL database, should the application need it.

If you used the starter service, then the generator has already been executed and you can deploy it's required services and then build and deploy the application.

## Deploy required services

If your application needs services such as a Database or Message Queue, this section shows you how to deploy these services to Kubernetes


### MySQL

**Step 1:** Create a secret:

```
kubectl create secret generic mysql \
  --from-literal=mysql-root-password=$(echo $RANDOM) \
  --from-literal=mysql-password=$(echo $RANDOM)
```

**Step 2:** Deploy the service"

```
kubectl apply -f kubernetes/services/mysql
```

#### Deleting Resources
To recreate the secret, first delete the existing secret:

```
kubectl delete secret mysql
```
To delete the database storage, delete the persistent volume:

```
kubectl delete pvc mysql
```

To delete the MySQL service and deployment in addition to the persistent volume:

```
kubectl delete deployment,services,pvc -l app=mysql
```

## Building and deploying the application

This generator relies on using the new `buildpack` support added in Spring Boot version 2.3 to create a container image.

If you are using Minikube you should configure your terminal to use the same Docker environment:

```bash
eval $(minikube docker-env)
```

**Step 1:** Build the project and create the container image:

```
./mvnw clean package spring-boot:build-image
```

**Step 2:** Deploy the app to Kubernetes

```
kubectl apply -f kubernetes/app
```

Use `kubectl get all` to verify that the resources created.

Accessing the application's endpoint varies based on the type of Kubernetes cluster you are using.  For example, if minikube is being used, look for the endpoint to access using the command `minikube service list`

The README.md file from the code repository for the appliation should include a few `curl` commands to exercise the application.



# Generator Information

This generator creates the Kubernetes `service` and `deploymnet` resources files to deploy a Spring Boot application using `kubectl`

To use the generator you will need to install the following command line tool:

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)


## Generator Commands

These commands use the `tss` CLI.

`tss k8s-simple new` creates

* A `kubernetes` directory with a `service.yaml` and `deployment.yaml`

`tss k8s-simple new-services` creates

* A `kubernetes/services/<service-name>` directory with Kubernetes resource files for various services.  Currently only `mysql` service name is supported.


## Generator installation

```
tss generator install --go-getter-url=github.com/markpollack/generator-k8s-simple
```

To use the install command you need to install [go-getter](https://github.com/hashicorp/go-getter#installation-and-usage) CLI.
