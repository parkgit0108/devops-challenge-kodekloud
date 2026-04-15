```sql
#Create secret
kubectl create secret generic official --from-file=license=/opt/official.txt

#This creates:
Secret name: official
Key inside secret: license
Value: content of file

#Verify secret
kubectl get secret official
kubectl describe secret official
```
```sql
#Create Pod YAML
vi secret-nautilus.yaml

apiVersion: v1
kind: Pod
metadata:
  name: secret-nautilus
spec:
  containers:
  - name: secret-container-nautilus
    image: ubuntu:latest
    command: ["/bin/bash", "-c"]
    args:
      - sleep 3600
    volumeMounts:
    - name: secret-volume
      mountPath: /opt/cluster

  volumes:
  - name: secret-volume
    secret:
      secretName: official
```
```sql
#Apply pod
kubectl apply -f secret-nautilus.yaml
#Check pod status
kubectl get pods
Wait until:
STATUS = Running
#Verify secret inside container
kubectl exec -it secret-nautilus -- /bin/bash

#Then inside pod
cd /opt/cluster
ls
cat license
```
