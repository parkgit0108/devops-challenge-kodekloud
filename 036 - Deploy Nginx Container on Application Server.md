ssh into app server and run below commands

```sql
docker run -d --name nginx_1 nginx:alpine
#Verify the container is running:
docker ps
```

NOTE:

-d → runs the container in detached (background) mode

--name nginx_1 → assigns the required container name

nginx:alpine → uses the lightweight Alpine-based Nginx image
