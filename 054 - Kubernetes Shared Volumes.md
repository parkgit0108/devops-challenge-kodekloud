```sql
#create the Pod YAML

cat > volume-share-devops.yaml << 'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-devops
spec:
  volumes:
    - name: volume-share
      emptyDir: {}

  containers:
    - name: volume-container-devops-1
      image: ubuntu:latest
      command: ["bash", "-c", "sleep 3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/beta

    - name: volume-container-devops-2
      image: ubuntu:latest
      command: ["bash", "-c", "sleep 3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/apps
EOF
```
```sql
#Create the Pod
kubectl apply -f volume-share-devops.yaml
#Verify Pod is running
kubectl get pods
#Exec into first container and create file
kubectl exec -it volume-share-devops -c volume-container-devops-1 -- bash
echo "Welcome to xFusionCorp Industries" > /tmp/beta/beta.txt
exit

#Verify file in second container
kubectl exec -it volume-share-devops -c volume-container-devops-2 -- cat /tmp/apps/beta.txt
#Expected output
Welcome to xFusionCorp Industries
```
