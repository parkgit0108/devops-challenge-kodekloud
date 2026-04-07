# Linux SSH Authentication

---

<aside>

**Purpose:** Generate an SSH key pair on the jump server and configure key-based SSH authentication to app servers.

</aside>

---

### Procedure

#### Task 1: Generate an SSH key on the jump server

1. Generate a key pair:
    
    ```
    ssh-keygen -t rsa -b 4096
    ```
    
    This creates a private key and a public key. Distribute the **public** key to the target app servers for the relevant user.
    

#### Task 2: Copy the public key to each app server (preferred)

1. Run (repeat for each app server):
    
    ```
    ssh-copy-id user@server-ip
    ```
    
    Example:
    
    ```
    ssh-copy-id steve@stapp02
    ```
    

#### Task 3: Copy the public key manually (if `ssh-copy-id` is unavailable)

1. Pipe the public key to `authorized_keys`:
    
    ```
    cat ~/.ssh/id_rsa.pub | ssh user@server-ip "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
    ```
    

#### Task 4: Add the key by logging into the server (fallback)

1. SSH into each app server.
2. Create the `.ssh` directory and edit `authorized_keys`:
    
    ```
    mkdir -p ~/.ssh
    vi ~/.ssh/authorized_keys
    ```
    
3. Copy the `id_rsa.pub` contents from the jump host and paste into `~/.ssh/authorized_keys`.

### Quick check

- **Expected result:** You can SSH to the app server without being prompted for the account password.
    
    ```
    ssh user@server-ip
    ```