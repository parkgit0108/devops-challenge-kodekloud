ssh into app server and follw the below commands

```sql
#switch to root user
sudo -i
```
```sql
#create docker compose file
sudo cat > /opt/devops/docker-compose.yml << 'EOF'
version: "3.8"

services:
  web:
    container_name: php_host
    image: php:apache
    ports:
      - "6100:80"
    volumes:
      - /var/www/html:/var/www/html

  db:
    container_name: mysql_host
    image: mariadb:latest
    ports:
      - "3306:3306"
    volumes:
      - /var/lib/mysql:/var/lib/mysql
    environment:
      MYSQL_DATABASE: database_host
      MYSQL_USER: nautuser
      MYSQL_PASSWORD: Nautilus@12345
      MYSQL_ROOT_PASSWORD: Root@12345
EOF
```
```sql
#start container
cd /opt/devops
docker compose up -d
```
