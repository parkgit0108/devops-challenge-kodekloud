ssh into app server and run below commands

```sql
#create docker network
docker network create \
  --driver bridge \
  --subnet 172.168.0.0/24 \
  --ip-range 172.168.0.0/24 \
  blog
```
```sql
#verify
docker network ls
docker network inspect blog
```
