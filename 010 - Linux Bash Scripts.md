# Linux Bash Scripts

---

<aside>

**Purpose:** Quick Linux bash / DevOps lab snippets (SSH keys + backup/transfer).

</aside>

---

### Procedure

#### Task 1: SSH into app server 3 and generate SSH key

1. SSH into the server (example):
    
    ```bash
    ssh <user>@<app-server-3>
    ```
    
2. Generate an SSH key:
    
    ```bash
    ssh-keygen -t rsa -b 4096
    ```
    

#### Task 2: Copy the SSH key to the target server

1. Copy the public key to the server stated in the lab:
    
    ```bash
    ssh-copy-id user@server-ip
    ```
    

#### Task 3: Create a zip backup

1. Zip the target directory:
    
    ```bash
    zip -r /backup/xfusioncorp_beta.zip /var/www/html/beta
    ```
    

#### Task 4: Copy the backup to the backup server

1. Copy the zip file to the backup server stated in the lab:
    
    ```bash
    scp /backup/xfusioncorp_beta.zip natasha@ststor01:/backup/
    ```
    

---

### Quick check

- **Expected result:** The key is installed on the target host, and `/backup/xfusioncorp_beta.zip` exists on `ststor01:/backup/`.