# K8s tools in Docker

Docker images with pre-installed tools

Base image: `ubuntu:bionic`

## Kubectl Usage

- Build image:

```sh
docker build -t kubectl .
```

- Run command examples:

```sh
docker run -it --rm exciter86/kubectl:1.18.2 kubectl version
docker run -it --rm exciter86/kubectl:1.18.2 gcloud --version
docker run -it --rm exciter86/kubectl:1.18.2 bq version

docker run --rm --name kubectl \
    -v ${PWD}/config:/kube/config exciter86/kubectl:1.18.2 \
    kubectl get pod --all-namespaces \
    --kubeconfig=/kube/config
```
