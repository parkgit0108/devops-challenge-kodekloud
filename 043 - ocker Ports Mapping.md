ssh into app server and run below commnads

```sql
#pull image
docker pull nginx:alpine-perl
```
```sql
#run image with required setting
docker run -d \
  --name demo \
  -p 8087:80 \
  nginx:alpine-perl
```
