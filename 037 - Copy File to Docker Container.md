ssh into app server and run below commnads

```sql
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/

#verify
docker exec ubuntu_latest ls -l /opt/
```

NOTE:

/tmp/nautilus.txt.gpg → source file on the host

ubuntu_latest → target container

/opt/ → destination directory inside the container

docker cp → copies the file as is (no modification)
