```sql
ssh max@ststor01
# Password: Max_pass123
cd /home/max/story-blog
git pull origin master
vi story-index.txt
# fix typo and remove conflict markers e.g. only the below should be in the file.
#1. The Lion and the Mouse
#2. The Frogs and the Ox
#3. The Fox and the Grapes
#4. The Donkey and the Dog

git add story-index.txt 
git commit -m "Resolve merge conflict and fix typo"
git push origin master
```
