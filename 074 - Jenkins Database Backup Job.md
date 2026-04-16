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
```
```sqld
#Tick excute shell and paste this
DATE=$(date +%F)
DUMP_FILE="db_${DATE}.sql"

ssh tony@stapp01 "mysqldump -u kodekloud_roy -pasdfgdsd kodekloud_db01 > /tmp/${DUMP_FILE}"

ssh natasha@ststor01 "mkdir -p /home/natasha/db_backups"

scp tony@stapp01:/tmp/${DUMP_FILE} natasha@ststor01:/home/natasha/db_backups/
```
```sql
#apply and build
```
