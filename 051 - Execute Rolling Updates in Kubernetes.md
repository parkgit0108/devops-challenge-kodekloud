```sql
#check the container name
kubectl get deployment nginx-deployment -o yaml

#run
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18
```
