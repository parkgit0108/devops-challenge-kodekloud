ssh into app server and run below commands.

```sql
#pull image
docker pull busybox:musl
#re tage image
docker tag busybox:musl busybox:blog
#verify
docker images | grep busybox

#you should see both
busybox:musl
busybox:blog
```

