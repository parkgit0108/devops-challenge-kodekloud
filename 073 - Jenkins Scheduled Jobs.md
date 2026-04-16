```sql
#generate passwordless ssh key in jenkins server and copy to storage and app server
ssh-keygen -t rsa
ssh-copy-id tony@stapp01
ssh-copy-id natasha@ststor01
```
```sql
#login to Jenkins and create job name copy-logs
#Tick build periodically
#Enter this cron expression for every 12 minutes
H/12 * * * *

#Tick excute shell and paste this
ssh tony@stapp01 "sudo cp /var/log/httpd/access_log /tmp/access_log && sudo cp /var/log/httpd/error_log /tmp/error_log && sudo chmod 644 /tmp/access_log /tmp/error_log"

scp tony@stapp01:/tmp/access_log natasha@ststor01:/home/natasha/
scp tony@stapp01:/tmp/error_log natasha@ststor01:/home/natasha/

ssh natasha@ststor01 "sudo mkdir -p /usr/src/security && sudo cp /home/natasha/access_log /usr/src/security/access_log && sudo cp /home/natasha/error_log /usr/src/security/error_log"
```
```sql
#apply and build
```
