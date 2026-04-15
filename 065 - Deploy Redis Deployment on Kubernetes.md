```sql
#Create ConfigMap using vi
vi redis-configmap.yaml
```
```sql
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-redis-config
data:
  redis-config: |
    maxmemory 2mb
Save and exit
```
```sql
#Apply ConfigMap
kubectl apply -f redis-configmap.yaml
```
```sql
#Create Deployment using vi
vi redis-deployment.yaml

Press i and paste:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: redis-container
        image: redis:alpine
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "1"
        volumeMounts:
        - name: data
          mountPath: /redis-master-data
        - name: redis-config
          mountPath: /redis-master
      volumes:
      - name: data
        emptyDir: {}
      - name: redis-config
        configMap:
          name: my-redis-config
Save and exit
```
```sql
#Apply
kubectl apply -f redis-deployment.yaml
#Verify
kubectl get deployments
kubectl get pods
#Confirm Pod is Running
kubectl describe pod <pod-name>
```
