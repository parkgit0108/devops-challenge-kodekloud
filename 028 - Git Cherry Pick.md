# Git Cherry Pick

---

<aside>

**Purpose:** Cherry-pick a specific commit from a feature branch into master on the storage server, then push the updated master.

</aside>

---

### Procedure

#### Task 1: SSH into the storage server

1. SSH into the storage server.

#### Task 2: Switch to root and move into the repository directory

1. Switch to root and change into the repo directory:
    
    ```bash
    sudo su
    cd /usr/src/kodekloudrepos/demo
    ```
    

#### Task 3: Find the commit hash on the feature branch

1. On the feature branch, find the commit hash you need:
    
    ```bash
    git log
    ```
    

#### Task 4: Switch to the master branch

1. Checkout master:
    
    ```bash
    git checkout master
    ```
    

#### Task 5: Update master from remote

1. Pull the latest changes:
    
    ```bash
    git pull origin master
    ```
    

#### Task 6: Cherry-pick the commit

1. Cherry-pick the required commit:
    
    ```bash
    git cherry-pick <commit-hash>
    ```
    

#### Task 7: Push master to remote

1. Push the updated master branch:
    
    ```bash
    git push origin master
    ```
    

---

### Reference

```bash
sudo su
cd /usr/src/kodekloudrepos/demo
git log
git checkout master
git pull origin master
git cherry-pick <commit-hash>
git push origin master
```