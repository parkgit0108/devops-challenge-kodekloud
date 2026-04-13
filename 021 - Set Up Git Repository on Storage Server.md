# Set Up Git Repository on Storage Server

1. ssh into ststor01 server
2. run below command

```sql
ssh natasha@ststor01
sudo yum install git -y
sudo mkdir -p /opt/news.git
sudo git init --bare /opt/news.git
```