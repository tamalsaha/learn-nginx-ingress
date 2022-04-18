helm upgrade -i voyager-operator appscode/voyager \
  --version v2022.04.13 \
  --namespace voyager --create-namespace \
  --set cloudProvider=linode \
  --set ingressClass=voyager \
  --set-file license=/Users/tamal/Downloads/voyager-enterprise-license-c586d5aa-e885-4402-b1b8-2a37cc55085d.txt

