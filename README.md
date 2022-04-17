# learn-nginx-ingress

- Need to port-forward for Mac m1
- https://kind.sigs.k8s.io/docs/user/ingress/#ingress-nginx

```
> kind create cluster --config=kind.yaml
> kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

```
