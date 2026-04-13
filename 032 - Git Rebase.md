SSH into storage server and run below command

```sql
sudo -i
cd /usr/src/kodekloudrepos/apps
git branch
git rebase master
git push origin feature --force
```
