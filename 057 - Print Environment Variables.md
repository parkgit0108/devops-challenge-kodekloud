```sql
#create the pod YAML
vi print-envars-greeting.yaml
```
```sql
#Paste below

apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  restartPolicy: Never
  containers:
    - name: print-env-container
      image: bash
      command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']
      env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "xFusionCorp"
        - name: GROUP
          value: "Ltd"
```
```sql
#apply and verify
kubectl apply -f print-envars-greeting.yaml
kubectl logs -f print-envars-greeting
```
