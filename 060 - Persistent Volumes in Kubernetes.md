```sql
vi devops.yaml
```
```sql
#paste below

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
spec:
  capacity:
    storage: 4Gi
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  hostPath:
    path: /mnt/security
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  resources:
    requests:
      storage: 2Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-devops
  labels:
    app: web-devops
spec:
  containers:
  - name: container-devops
    image: nginx:latest
    ports:
    - containerPort: 80
    volumeMounts:
    - name: web-storage
      mountPath: /usr/share/nginx/html
  volumes:
  - name: web-storage
    persistentVolumeClaim:
      claimName: pvc-devops
---
apiVersion: v1
kind: Service
metadata:
  name: web-devops
spec:
  type: NodePort
  selector:
    app: web-devops
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```
```sql
#apply and verify
kubectl apply -f devops.yaml
kubectl get pv
kubectl get pvc
kubectl get pods
kubectl get svc
```
