# Git Create Branches

---

<aside>

**Purpose:** Create a new Git branch from `master` in the lab repo.

</aside>

---

### Procedure

#### Task 1: SSH into the storage server

1. SSH into the storage server (as specified in the lab).

#### Task 2: Switch to the repo directory

1. Become root (if required):
    
    ```bash
    sudo su
    ```
    
2. Go to the cluster repo directory:
    
    ```bash
    cd /usr/src/kodekloudrepos/cluster
    ```
    

#### Task 3: Ensure you are on `master`

1. Check the current branch:
    
    ```bash
    git branch
    ```
    
2. Switch to `master` (if not already):
    
    ```bash
    git checkout master
    ```
    

#### Task 4: Create the new branch

1. Create and switch to the new branch `xfusioncorp_cluster`:
    
    ```bash
    git checkout -b xfusioncorp_cluster
    ```
    

---

### Quick check

- Confirm you are on the new branch:
    
    ```bash
    git branch
    ```