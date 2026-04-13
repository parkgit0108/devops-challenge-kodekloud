# Git Reset Hard

---

<aside>

**Purpose:** Reset the ecommerce repository to a specified commit using a hard reset, then force-push the updated history.

</aside>

---

### Procedure

#### Task 1: SSH into the storage server and move into the repository

1. Switch to root and change into the repo directory:
    
    ```bash
    sudo -i
    cd /usr/src/kodekloudrepos/ecommerce
    ```
    

#### Task 2: Check commit history and note the target hash

1. View the commit history:
    
    ```bash
    git log --oneline
    ```
    
2. Note the commit message provided by the lab instructions and find the hash number.

#### Task 3: Hard reset to the target commit

1. Reset to the required commit hash:
    
    ```bash
    git reset --hard <hash>
    ```
    
2. Verify working tree is clean:
    
    ```bash
    git status
    ```
    

#### Task 4: Force-push the changes

1. Force-push to update the remote history:
    
    ```bash
    git push --force
    ```
    

---

### Reference

```bash
sudo -i
cd /usr/src/kodekloudrepos/ecommerce
git log --oneline
git reset --hard <hash>
git status
git push --force
```