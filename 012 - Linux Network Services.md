# Linux Network Services

---

<aside>

**Purpose:** Free up port **5004** for Apache (`httpd`), restart the service, confirm it’s listening, and allow traffic via `iptables`.

</aside>

---

### Procedure

#### Task 1: SSH to the app server and confirm what is using port 5004

1. SSH to the relevant app server.
2. Check which process is listening on port 5004:
    
    ```
    sudo netstat -tulnp | grep 5004
    ```
    
    If `netstat` is not available:
    
    ```
    sudo yum install -y net-tools
    ```
    
    You should see output similar to:
    
    ```
    tcp   LISTEN  0  128  0.0.0.0:5004  ...  PID/process
    ```
    

#### Task 2: Kill the process using port 5004 (if it should be Apache)

1. Kill the process using the PID from the previous step:
    
    ```
    sudo kill -9 <PID>
    ```
    

#### Task 3: Restart Apache and verify service status

1. Restart `httpd`:
    
    ```
    sudo systemctl restart httpd
    ```
    
2. Confirm it is active:
    
    ```
    sudo systemctl status httpd
    ```
    

#### Task 4: Confirm Apache is listening on port 5004

1. Re-check the listening port and confirm the owning process is `httpd`:
    
    ```
    sudo netstat -tulnp | grep 5004
    ```
    

#### Task 5: Allow inbound traffic to port 5004 (iptables)

1. Insert an allow rule for TCP/5004:
    
    ```
    iptables -I INPUT 4 -p tcp --dport 5004 -j ACCEPT
    ```
    

### Quick check

- Test locally on the app server:
    
    ```
    curl http://localhost:5004/
    ```
    
- Test from the jump host:
    
    ```
    curl http://stapp03:5004/
    ```