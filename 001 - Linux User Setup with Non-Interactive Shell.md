# Linux User Setup with Non-Interactive Shell

---

<aside>

**Purpose:** Create a Linux user account with a non-interactive (nologin) shell, and verify that the account cannot be used for an interactive login.

</aside>

---

### Procedure

#### Task 1: SSH into the server

1. SSH to the server:
    
    ```
    ssh <user>@hostname
    
    #example
    ssh steve@app02
    ```
    
2. Enter the password when prompted.

#### Task 2: Create the user with a non-interactive shell

1. Create the user (with a home directory) and set the shell to `nologin`:
    
    ```
    sudo useradd -m -s /usr/sbin/nologin user-name
    ```
    
2. Notes:
    - `-s`: sets the login shell (here, `nologin`)
    - `-m`: creates the home directory (e.g., `/home/user-name`)

#### Task 3: Verify the result

1. Confirm the user entry exists in `/etc/passwd`:
    
    ```
    cat /etc/passwd
    ```
    
    - Example entry:
        
        ```
        user-name:x:1003:1004::/home/user-name:/usr/sbin/nologin
        ```
        
2. Attempt to switch to the user:
    
    ```
    sudo su user-name
    ```
    
    - Expected output:
        
        ```
        This account is currently not available.
        ```
        

### Quick check

- **Expected result:** The user exists, has `/usr/sbin/nologin` as the shell, and interactive login is blocked.