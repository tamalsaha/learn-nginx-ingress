# Test TCP Proxy

```
> kind create cluster
```

```
> helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
> helm repo update
```

```
> wget https://github.com/kubernetes/ingress-nginx/raw/controller-v1.1.3/rootfs/etc/nginx/template/nginx.tmpl
> kubectl create configmap ingress-nginx-tmpl -n ace --from-file=nginx.tmpl

--set controller.customTemplate.configMapName=ingress-nginx-tmpl \
--set controller.customTemplate.configMapKey=nginx.tmpl
```

```
helm upgrade -i ingress-nginx ingress-nginx/ingress-nginx  \
--namespace ace --create-namespace \
--set controller.ingressClassResource.name=nginx-ace \
--set controller.ingressClassResource.controllerValue="appscode.com/ingress-nginx" \
--set controller.ingressClassResource.enabled=true \
--set controller.ingressClass=nginx-ace \
--set controller.ingressClassByName=true \
--set tcp.9443="ace/web:8080" \
--set controller.customTemplate.configMapName=ingress-nginx-tmpl \
--set controller.customTemplate.configMapKey=nginx.tmpl
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



```
> wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/rootfs/etc/nginx/template/nginx.tmpl

```



kubectl create configmap ingress-nginx-tmpl -n default --from-file=nginx.tmpl

helm upgrade -i ingress-nginx ingress-nginx/ingress-nginx  \
--namespace default --create-namespace \
--set controller.ingressClassResource.name=ingress-nginx \
--set controller.ingressClassResource.controllerValue="k8s.io/ingress-nginx" \
--set controller.ingressClassResource.enabled=true \
--set controller.ingressClass=nginx \
--set controller.ingressClassByName=true \
--set controller.watchIngressWithoutClass=true \
--set tcp.4222="bb/nats-server:4222" \
--set tcp.6443="demo/test-server:6443" \
--set tcp.4343="demo/test-server:4343" \
--set tcp.6767="demo/test-server:6767" \
--set controller.customTemplate.configMapName=ingress-nginx-tmpl \
--set controller.customTemplate.configMapKey=nginx.tmpl




> kubectl create configmap ingress-nginx-tmpl -n default --from-file=nginx.tmpl
configmap/ingress-nginx-tmpl created

> helm ls
NAME         	NAMESPACE	REVISION	UPDATED                                  	STATUS  	CHART               	APP VERSION
ingress-nginx	default  	5       	2022-02-25 17:43:05.704149237 +0600 +0600	deployed	ingress-nginx-4.0.17	1.1.1

# run helm upgrade

> helm ls
NAME         	NAMESPACE	REVISION	UPDATED                             	STATUS  	CHART               	APP VERSION
ingress-nginx	default  	6       	2022-04-17 12:10:26.955273 -0700 PDT	deployed	ingress-nginx-4.0.19	1.1.3



> k exec -it -n default deploy/ingress-nginx-controller -- cat /etc/nginx/nginx.conf > nginx-ninja.conf


http://nginx.org/en/docs/stream/ngx_stream_ssl_preread_module.html

https://52.23.215.245.nip.io/

https://serversforhackers.com/c/tcp-load-balancing-with-nginx-ssl-pass-thru


## nats probe

https://docs.nginx.com/nginx/admin-guide/load-balancer/tcp-health-check/

    livenessProbe:
      failureThreshold: 3
      httpGet:
        path: /
        port: 8222
        scheme: HTTP
      initialDelaySeconds: 10
      periodSeconds: 30
      successThreshold: 1
      timeoutSeconds: 5

