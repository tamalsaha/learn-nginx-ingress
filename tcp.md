# Test TCP Proxy

```
> kind create cluster
```

```
> helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
> helm repo update
```

```
helm upgrade -i ingress-nginx ingress-nginx/ingress-nginx  \
--namespace ace --create-namespace \
--set controller.ingressClassResource.name=nginx-ace \
--set controller.ingressClassResource.controllerValue="appscode.com/ingress-nginx" \
--set controller.ingressClassResource.enabled=true \
--set controller.ingressClass=nginx-ace \
--set controller.ingressClassByName=true \
--set tcp.9443="ace/web:8080"
```

```
> kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0 -n ace
> kubectl expose deployment web --type=ClusterIP --port=8080 -n ace
```

- Port forward ingress-nginx svc

```
k port-forward svc/ingress-nginx-controller 9443:9443 -n ace
```

```
> curl localhost:9443
Hello, world!
Version: 1.0.0
Hostname: web-746c8679d4-h2vkj
```
