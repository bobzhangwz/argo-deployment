```bash
kubectl create -n argo secret docker-registry aws-rds-secret \
  --docker-username AWS \
  --docker-password "$(aws --region ap-northeast-1 ecr get-login-password)" \
  --docker-server "https://160071257600.dkr.ecr.ap-northeast-1.amazonaws.com"
```
