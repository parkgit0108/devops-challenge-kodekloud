ssh into app server and run following commands

```sql
#Install Docker CE & add Docker repository
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
#Install Docker packages
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
#Enable and Start Docker Service
sudo systemctl enable docker
sudo systemctl start docker
#Verify Installation
docker --version
docker compose version
sudo systemctl status docker
```
