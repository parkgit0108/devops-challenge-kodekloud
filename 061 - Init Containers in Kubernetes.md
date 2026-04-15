```sql
vi ic-deploy-datacenter.yaml
```
```sql
#init setup

apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-datacenter
  template:
    metadata:
      labels:
        app: ic-datacenter
    spec:
      volumes:
      - name: ic-volume-datacenter
        emptyDir: {}

      initContainers:
      - name: ic-msg-datacenter
        image: fedora:latest
        command: ["/bin/bash", "-c"]
        args:
          - echo Init Done - Welcome to xFusionCorp Industries > /ic/news
        volumeMounts:
        - name: ic-volume-datacenter
          mountPath: /ic

      containers:
      - name: ic-main-datacenter
        image: fedora:latest
        command: ["/bin/bash", "-c"]
        args:
          - while true; do cat /ic/news; sleep 5; done
        volumeMounts:
        - name: ic-volume-datacenter
          mountPath: /ic
```
```sql
#apply and verify
kubectl apply -f ic-deploy-datacenter.yaml
kubectl get pods
kubectl describe pod <pod-name>

#Check logs
kubectl logs <pod-name>

#You should see
Init Done - Welcome to xFusionCorp Industries
```
