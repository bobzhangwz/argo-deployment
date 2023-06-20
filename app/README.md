
```yaml
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
```

```bash
kubectl delete secret aws-rds-secret -n argo
# create a secret in helloworld
kubectl create -n argo secret docker-registry aws-rds-secret \
  --docker-username AWS \
  --docker-password "$(aws --region ap-northeast-1 ecr get-login-password)" \
  --docker-server "https://160071257600.dkr.ecr.ap-northeast-1.amazonaws.com"
```
