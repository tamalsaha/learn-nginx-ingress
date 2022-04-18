helm upgrade -i voyager-operator appscode/voyager \
  --version v2022.04.13 \
  --namespace voyager --create-namespace \
  --set cloudProvider=linode \
  --set ingressClass=voyager \
  --set-file license=/Users/tamal/Downloads/voyager-enterprise-license-c586d5aa-e885-4402-b1b8-2a37cc55085d.txt


k apply -f voyager-ingress.yaml

nats --server tls://nats.appscode.ninja:4222 stream report --creds=/Users/tamal/Desktop/admin-user.cred



[8] 2022/04/18 02:39:04.982021 [ERR] 10.2.1.42:38788 - cid:762 - TLS handshake error: read tcp 10.2.4.3:4222->10.2.1.42:38788: i/o timeout

