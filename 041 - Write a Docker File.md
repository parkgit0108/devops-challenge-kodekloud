ssh into app server and run belo commands

```sql
#switch to root user
sudo -i
```
```sql
#create Dockerfile

cat > /opt/docker/Dockerfile << 'EOF'
FROM ubuntu:24.04

RUN apt-get update && apt-get install -y apache2

RUN sed -i 's/Listen 80/Listen 5002/' /etc/apache2/ports.conf

EXPOSE 5002

CMD ["apachectl", "-D", "FOREGROUND"]
EOF
```
```sql
#build the image
cd /opt/docker
docker build -t custom-apache:latest .

#run
docker run -d -p 5002:5002 --name apache_test custom-apache:latest
```
