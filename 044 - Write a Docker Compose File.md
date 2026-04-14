ssh into app server and run following commands.

```sql
#switch to root user
sudo -i
```
```sql
#create docker compose file
cat > /opt/docker/docker-compose.yml << 'EOF'
version: "3.8"

services:
  web:
    image: httpd:latest
    container_name: httpd
    ports:
      - "3000:80"
    volumes:
      - /opt/dba:/usr/local/apache2/htdocs
EOF
```
```sql
#start the container using the docker compose
cd /opt/docker
docker compose up -d
```
