# Git Revert Some Changes

---

<aside>

**Purpose:** Revert the latest commit in the apps repository on the storage server and verify the history.

</aside>

---

### Procedure

#### Task 1: SSH into the storage server

1. SSH into the storage server.

#### Task 2: Switch to root and move into the repository directory

1. Switch to root and change into the repo directory:
    
    ```bash
    sudo su
    cd /usr/src/kodekloudrepos/apps
    ```
    

#### Task 3: Check the git log (find the commits)

1. View the commit history:
    
    ```bash
    git log --oneline
    ```
    
2. Identify the latest commit (HEAD) you want to revert.

#### Task 4: Revert the latest commit

1. Revert the latest commit:
    
    ```bash
    git revert HEAD --no-edit
    ```
    
2. (If required) amend the commit message:
    
    ```bash
    git commit --amend -m "revert apps"
    ```
    

#### Task 5: Verify

1. Confirm the new revert commit is on top:
    
    ```bash
    git log --oneline -2
    ```
    

---

### Reference

```bash
sudo su
cd /usr/src/kodekloudrepos/apps
git log --oneline
git revert HEAD --no-edit
git commit --amend -m "revert apps"
git log --oneline -2
```