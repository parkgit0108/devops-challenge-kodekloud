```sql
#identify the issues
kubectl get svc python-deployment-devops -o yaml
kubectl get deployment python-deployment-devops -o yaml

#my issue and fixes
#Root Cause

image: poroko/flask-app-demo
#the correct imageis
poroko/flask-demo-app

#Correct the image
kubectl set image deployment python-deployment-devops \
python-container-devops=poroko/flask-demo-app
#Restart rollout
kubectl rollout restart deployment python-deployment-devops
#Check pods
kubectl get pods
#Wait until
STATUS: Running
READY: 1/1

#make sure the target port is 5000
#find service name
kubectl get svc
kubectl edit svc <service-name>

nodePort: 32345
targetPort: 5000

#confirm endpoint exists
kubectl get endpoints python-service-devops
```
