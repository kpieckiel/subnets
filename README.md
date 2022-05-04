# subnets
Visual subnet calculator as seen at http://www.davidc.net/sites/default/subnets/subnets.html

# Run with docker

```
cd <project folder>
docker build . -t subnets
docker run -d -p 5001:80 --name subnets subnets
```

# Kubernetes

## Prerequesits
This guide assumes a kubernetes cluster exits and you have a kubecfg that allows
management via `kubectl` commands. Ingress also assumes that you are using the 
[NGINX Ingress Controller](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-helm/).

## Namespace
Before deploying, consider creating and switching to a new namespace for this project. For example with kubectl

```shell
kubectl create namespace kwlug
kubectl config set-context --current --namespace=kwlug
```

## deploy
Deploy in one easy step!

```shell
helm install --generate-name subnet-chart --set domain=arrakis.jskw.ca
```

## Undeploy
You can cleanup your deployment(s) with the `helm uninstall` command:

### Delete single release
```shell
helm uninstall subnet-chart-1651426690
```

### Delete all releases

```shell
helm list --output json | \
    jq '.[].name' --raw-output | \
    grep subnet-chart | \
    xargs helm uninstall
```