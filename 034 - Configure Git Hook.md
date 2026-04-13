ssh to storage server and switch to root user
```sql
cd /opt/media.git/hooks
cp post-update.sample post-update
vi post-update
#replace the content with below

#!/usr/bin/sh

# Arguments to post-update
DATE=$(date +%F)        # YYYY-MM-DD
GIT_DIR=$(pwd)

        echo "Creating tag release-$DATE"
        git --git-dir="$GIT_DIR" tag "release-$DATE" master

chmod +x /opt/media.git/hooks/post-update
cd /usr/src/kodekloudrepos/media

git checkout master
git merge feature
git push

#verify
git fetch --tags
git tag
```
