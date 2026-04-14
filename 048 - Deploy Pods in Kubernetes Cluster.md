```sql
#create Pod YAML file
cat > pod-nginx.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: pod-nginx
  labels:
    app: nginx_app
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
EOF
```
```sql
#Create the pod in the cluster
kubectl apply -f pod-nginx.yaml
#Verify pod status
kubectl get pods
#For detailed info
kubectl describe pod pod-nginx
```
