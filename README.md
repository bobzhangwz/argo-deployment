refer to https://github.com/viaduct-ai/kustomize-sops

```bash

age-keygen -o key.txt

sops --encrypt --age <text.publickey> secret.yaml > secret.enc.yaml

# SOPS_AGE_KEY_FILE=./key.txt helm secret edit secret.enc.yaml
cat key.txt | kubectl create secret generic sops-age --namespace=argo \                                                                                                       <aws:twb>
--from-file=key.txt=/dev/stdin

cat <<EOF | sops --encrypt --age <age_key> /dev/stdin > app/github_token.enc.yaml
apiVersion: v1
kind: Secret
metadata:
  name: static-web-repo
  namespace: argo
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  type: git
  url: https://github.com/bobzhangwz/static-web
  password: 
  username: 
EOF

SOPS_AGE_KEY_FILE=./key.txt helmfile apply --skip-diff-on-install

# create a secret in helloworld
# https://github.com/argoproj-labs/argocd-image-updater/issues/112
# kubectl delete secret aws-rds-secret -n argo
kubectl create -n argo secret docker-registry aws-rds-secret \
  --docker-username AWS \
  --docker-password "$(aws --region ap-northeast-1 ecr get-login-password)" \
  --docker-server "https://160071257600.dkr.ecr.ap-northeast-1.amazonaws.com"

kubectl create -n helloworld secret docker-registry aws-rds-secret \
  --docker-username AWS \
  --docker-password "$(aws --region ap-northeast-1 ecr get-login-password)" \
  --docker-server "https://160071257600.dkr.ecr.ap-northeast-1.amazonaws.com"
```
