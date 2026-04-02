# Temporary User Setup with Expiry

---

<aside>

**Purpose:** Create a temporary Linux user account that automatically expires on a specified date.

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

#### Task 2: Create the user with an expiry date

1. Create the user (with a home directory) and set an expiry date:
    
    ```
    sudo useradd -m -e <date> user-name
    ```
    
2. Notes:
    - `-m`: creates the home directory (e.g., `/home/user-name`)
    - `-e`: sets the account expiry date (format is typically `YYYY-MM-DD`)
    - Replace `<date>` and `user-name` with your values

#### Task 3: Verify the result

1. Confirm the user entry exists in `/etc/passwd`:
    
    ```
    cat /etc/passwd
    ```
    
2. (Optional) Try switching to the user:
    
    ```
    sudo su user-name
    ```
    

### Quick check

- **Expected result:** The user exists, and the account will be disabled after the configured expiry date.