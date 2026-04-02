# Secure Root SSH Access

---

<aside>

**Purpose:** Disable direct root SSH login by setting `PermitRootLogin no` and restarting `sshd`.

</aside>

---

### Procedure

#### Task 1: SSH into the server

1. SSH to the server:
    
    ```
    ssh <user>@hostname
    
    #example
    ssh steve@stapp02
    ```
    
2. Enter the password when prompted.

#### Task 2: Disable root SSH login

1. Edit the SSH daemon config:
    
    ```
    sudo vi /etc/ssh/sshd_config
    ```
    
2. Find the line:
    
    ```
    PermitRootLogin yes
    ```
    
3. Change it to:
    
    ```
    PermitRootLogin no
    ```
    
4. Save and exit your editor - :wq!
5. Restart the SSH daemon:
    
    ```
    sudo systemctl restart sshd
    ```
    
6. Alternative (one-liner) update:
    
    ```
    sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
    sudo systemctl restart sshd
    ```
    

#### Task 3: Verify the result

1. Confirm the config is set as expected:
    
    ```
    grep -n '^PermitRootLogin' /etc/ssh/sshd_config
    ```
    
2. (Optional) Validate the SSH daemon config:
    
    ```
    sudo sshd -t
    ```
    

### Quick check

- **Expected result:** Root cannot SSH directly; access should be via a normal user + `sudo`.