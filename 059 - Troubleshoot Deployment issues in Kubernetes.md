```sql
#Check redis pod name
kubectl get pods
kubectl describe pod <redis-pod-name>
#look for the error message at bottom and for typos
#found typo in Image and wrong configmap
#FailedMount: configmap "redis-conig" not found
#Image: redis:alpin
#edit
kubectl edit deployment redis-deployment
#set image again and restart
kubectl set image deployment redis-deployment redis-container=redis:alpine
kubectl rollout restart deployment redis-deployment
#verify that is running
kubectl get pods
```


