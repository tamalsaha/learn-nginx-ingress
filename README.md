# learn-nginx-ingress

- Need to port-forward for Mac m1
- https://kind.sigs.k8s.io/docs/user/ingress/#ingress-nginx

```
> kind create cluster --config=kind.yaml
> kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

```

- https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
- https://github.com/kubernetes-sigs/kind/issues/99#issuecomment-732476241

```
> kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
deployment.apps/web created
> kubectl expose deployment web --type=ClusterIP --port=8080

> k apply -f ing.yaml
ingress.networking.k8s.io/example-ingress created

> k get svc -n ingress-nginx
NAME                                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                      AGE
ingress-nginx-controller             NodePort    10.96.241.76   <none>        80:30037/TCP,443:31426/TCP   2m33s
ingress-nginx-controller-admission   ClusterIP   10.96.40.202   <none>        443/TCP                      2m33s
```

```
> curl -H "Host:hello-world.info" localhost
Hello, world!
Version: 1.0.0
Hostname: web-746c8679d4-9gmvp
```

```
> k get pods -n ingress-nginx
NAME                                       READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-ncmw8       0/1     Completed   0          36m
ingress-nginx-admission-patch-njp9l        0/1     Completed   0          36m
ingress-nginx-controller-58fdb7bb4-fzgxb   1/1     Running     0          36m

> k exec -it -n ingress-nginx ingress-nginx-controller-58fdb7bb4-fzgxb -- cat /etc/nginx/nginx.conf > nginx.conf
```

- Install ingress-nginx kubectl plugin

```
> go build -v ./cmd/plugin/*.go
> sudo mv main /Users/tamal/.krew/bin/kubectl-ingress_nginx
```

- See backends

```
> kubectl ingress-nginx backends --list -n ingress-nginx
default-web-8080
upstream-default-backend

> kubectl ingress-nginx backends --backend=default-web-8080 -n ingress-nginx
```
