# Create a Cron Job

---

<aside>

**Purpose:** Install and enable cron (crond) on CentOS, then create and verify a root cron schedule.

</aside>

---

### Procedure

#### Task 1: Connect to the server(s)

1. SSH into each app server.

#### Task 2: Install cron service (cronie)

1. Install the `cronie` package:
    
    ```
    sudo yum install cronie -y
    ```
    

#### Task 3: Enable and start `crond`

1. Enable the service:
    
    ```
    sudo systemctl enable crond
    ```
    
2. Start the service:
    
    ```
    sudo systemctl start crond
    ```
    

#### Task 4: Create a cron schedule

1. Edit root’s crontab:
    
    ```
    sudo crontab -e
    ```
    
2. Add the schedule (runs every 5 minutes):
    
    ```
    */5 * * * * echo hello > /tmp/cron_text
    ```
    

#### Task 5: Verify

1. Confirm the crontab entry:
    
    ```
    sudo crontab -l
    ```
    
2. Wait ~5 minutes, then check the output file:
    
    ```
    cat /tmp/cron_text
    ```
    

### Quick check

- **Expected result:** `sudo crontab -l` shows the schedule, and `/tmp/cron_text` contains `hello` after a few minutes.