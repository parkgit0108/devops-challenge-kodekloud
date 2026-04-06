# Script Execution Permissions

---

<aside>

**Purpose:** Ensure the script at `/tmp/xfusioncorp.sh` is executable by updating its permissions to `755`.

</aside>

---

### Procedure

#### Task 1: SSH into the server

1. SSH to App server 3.

#### Task 2: Check current permissions

1. Check the current file permission status:
    
    ```
    ls -la /tmp
    ```
    
2. Confirm the script permissions look like this (non-executable):
    
    ```
    4 ---------- 1 root root   40 Jul 30 02:21 xfusioncorp.sh
    ```
    

#### Task 3: Update permissions

1. Run the following command to update permissions:
    
    ```
    sudo chmod 755 /tmp/xfusioncorp.sh
    ```
    

#### Task 4: Verify the result

1. Verify the results:
    
    ```
    ls -la /tmp
    ```
    
2. Confirm the updated permissions look like this (executable):
    
    ```
    4 -rwxr-xr-x 1 root root   40 Jul 30 02:21 xfusioncorp.sh
    ```
    

### Quick check

- **Expected result:** `/tmp/xfusioncorp.sh` shows `-rwxr-xr-x` permissions.