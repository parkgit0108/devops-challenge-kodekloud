```sql
#get pod YAML config
kubectl get pod nginx-phpfpm -o yaml > nginx-phpfpm.yml
#check nginix root directory in configmap data
kubectl get configmap -o yaml

#update container image mounth path to above.
vi nginx-phpfpm.yml

#recreate pod
kubectl delete pod nginx-phpfpm
kubectl apply -f nginx-phpfpm.yml

#copy index.php
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container

#test
curl localhost:8080
```
