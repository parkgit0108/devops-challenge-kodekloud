```sql
#Create the Pod definition

cat > httpd-pod.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
      resources:
        requests:
          memory: "15Mi"
          cpu: "100m"
        limits:
          memory: "20Mi"
          cpu: "100m"
EOF
```
```sql
#Create the Pod
kubectl apply -f httpd-pod.yaml
#Verify Pod status
kubectl get pods

#For detailed inspection
kubectl describe pod httpd-pod
```
