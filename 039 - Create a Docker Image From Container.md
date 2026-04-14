ssh into app server and run below commands.

```sql
docker commit ubuntu_latest demo:xfusion

#verify
docker images | grep demo
```

NOTE:

docker commit → creates a new image from a container

ubuntu_latest → source container

demo:xfusion → new image name and tag
