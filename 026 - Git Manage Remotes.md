# Git Manage Remotes

---

<aside>

**Purpose:** Add a new Git remote on the storage server, commit a file change, and push to the new remote.

</aside>

---

### Procedure

#### Task 1: SSH into the storage server

1. SSH into the storage server.

#### Task 2: Switch to root and move into the repo directory

1. Switch to root and change into the repo directory:
    
    ```bash
    sudo su
    cd /usr/src/kodekloudrepos/games
    ```
    

#### Task 3: Check current remotes and branch

1. Check the current remote(s) and branch:
    
    ```bash
    git remote -v
    git branch
    ```
    

#### Task 4: Add the new remote

1. Add the new remote and verify it was added:
    
    ```bash
    git remote add dev_beta /opt/xfusioncorp_games.git
    git remote -v
    ```
    

#### Task 5: Copy the file and commit changes

1. Copy the file, stage, and commit:
    
    ```bash
    cp /tmp/index.html .
    git add .
    git commit -m "added tmp file"
    ```
    

#### Task 6: Push the changes to the new remote

1. Push the changes:
    
    ```bash
    git push dev_beta master
    ```
    

---

### Reference

```bash
sudo su
cd /usr/src/kodekloudrepos/games
git remote -v
git branch
git remote add dev_beta /opt/xfusioncorp_games.git
git add .
git commit -m "added tmp file"
git push dev_beta master
```