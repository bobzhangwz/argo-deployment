refer to https://github.com/viaduct-ai/kustomize-sops

```bash

age-keygen -o key.txt

sops --encrypt --age <text.publickey> secret.yaml > secret.enc.yaml
# SOPS_AGE_KEY_FILE=./key.txt helm secret edit secret.enc.yaml
cat key.txt | kubectl create secret generic sops-age --namespace=argo \                                                                                                       <aws:twb>
--from-file=key.txt=/dev/stdin

SOPS_AGE_KEY_FILE=./key.txt helmfile apply --skip-diff-on-install
```
