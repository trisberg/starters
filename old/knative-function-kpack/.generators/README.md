# generator-knative-kpack-simple
Generator that creates a small set of Knative and Kpack manifest files for applications and its dependent services.

1. Building with Kpack/Tanzu Build Service
2. Deploying to Knative

**Note:** - For all the generated manifests, please adjust the image name to the container registry in use
* For local K8s - manifests work as-is
* For GCR, for example - image: gcr.io/<project_name>/<image-name>

## Building with Kpack / Tanzu Build Service
To build images in a declarative manner, provision the Kpack/TBS manifest for the type of image you wish to build: JVM/Native, by creating a Kpack/TBS image, based on the template generated in the `kubernetes` folder:
* JVM - /kubernetes/jvm/image.yaml 
* Native - /kubernetes/native/image-native.yaml

To build the service, please execute:
```shell
$ kubectl apply -f /kubernetes/jvm/image.yaml 

$ kubectl apply -f /kubernetes/jvm/image-native.yaml
```

To delete the build image for the service, please execute:
```shell
$ kubectl delete -f /kubernetes/jvm/image.yaml 

$ kubectl delete -f /kubernetes/jvm/image-native.yaml
```

## Deploying to Knative
To deploy the service to Knative, select the image you wish to deploy, generated in the `kubernetes` folder:
* JVM - /kubernetes/jvm/service.yaml 
* Native - /kubernetes/native/service-native.yaml

To deploy the service, please execute:
```shell
$ kubectl apply -f /kubernetes/jvm/service.yaml 

$ kubectl apply -f /kubernetes/jvm/service-native.yaml
```

To delete the service, please execute:
```shell
$ kubectl delete -f /kubernetes/jvm/service.yaml 

$ kubectl delete -f /kubernetes/jvm/service-native.yaml
```

