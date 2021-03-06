- https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/hostport.md

if $.Values.controller.hostPort.enabled

{{- if or (eq .Values.controller.kind "DaemonSet") 

controller.service.external.enabled=false

controller:
  kind: DaemonSet
  hostPort:
    enabled: true


```
> k create deployment web --image=gcr.io/google-samples/hello-app:1.0
deployment.apps/web created
> k expose deployment web --type=ClusterIP --port=8080

> k apply -f ing.yaml
ingress.networking.k8s.io/example-ingress created

helm upgrade -i ingress-nginx ingress-nginx/ingress-nginx  \
--namespace default --create-namespace \
--set controller.ingressClassResource.name=nginx \
--set controller.ingressClassResource.controllerValue="k8s.io/ingress-nginx" \
--set controller.ingressClassResource.enabled=true \
--set controller.ingressClassByName=true \
--set controller.kind=DaemonSet \
--set controller.hostPort.enabled=true \
--set controller.service.external.enabled=false
```

# Test nginx

```
> k port-forward ds/ingress-nginx-controller 8080:80

> curl -H "Host:hello-world.info" localhost:8080
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx</center>
</body>
</html>
```
