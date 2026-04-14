```sqld
#created deployment YAML file
cat > httpd-deployment.yaml << 'EOF'
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
        - name: httpd
          image: httpd:latest
EOF
```
```sql
#Apply the deployment
kubectl apply -f httpd-deployment.yaml
#Verify deployment
kubectl get deployments

C#heck pods created by the deployment
kubectl get pods
```
