# generator-knative-boot-native

Generator for Knative Resources deployed with Skaffold compiled as a GraalVM native image.

## Run the application

To start the application on a local cluster run:

```bash
skaffold run -p local --default-repo dev.local
```

To start the application on a remote cluster, set `DOCKER_ID` to your Docker Hub ID and then run:

```bash
skaffold run --default-repo $DOCKER_ID
```
