# IPtables Installation And Configuration

---

<aside>

**Purpose:** Install and configure `iptables` on Rocky Linux 8/9, allowing only the Load Balancer to reach a specific app port (example: `6200`), and persist rules across reboots.

</aside>

---

### Procedure

#### Task 1: Install iptables and the persistence service

1. Install packages:
    
    ```bash
    sudo dnf install -y iptables iptables-services
    ```
    

#### Task 2: Enable and start the iptables service

1. Enable the service at boot:
    
    ```bash
    sudo systemctl enable iptables
    ```
    
2. Start it now:
    
    ```bash
    sudo systemctl start iptables
    ```
    

#### Task 3: Flush any existing rules (start clean)

1. Flush rules:
    
    ```bash
    sudo iptables -F
    ```
    

#### Task 4: Find the Load Balancer (LB) IP

1. Resolve the LB hostname (replace `stlb01` as needed):
    
    ```bash
    getent hosts stlb01
    ```
    
2. Note the first IP in the output (example):
    
    ```
    172.16.238.14  stlb01
    ```
    

#### Task 5: Allow the LB to access the app port

Assume:

- App port = `6200`
- LB IP = `172.16.238.14`
1. Add an allow rule for the LB:
    
    ```bash
    sudo iptables -A INPUT -p tcp -s 172.16.238.14 --dport 6200 -j ACCEPT
    ```
    

#### Task 6: Block all other traffic to the app port

1. Add a drop rule for everyone else:
    
    ```bash
    sudo iptables -A INPUT -p tcp --dport 6200 -j DROP
    ```
    

#### Task 7: Save rules for persistence

1. Save the current ruleset (Rocky 8/9):
    
    ```bash
    sudo iptables-save | sudo tee /etc/sysconfig/iptables
    ```
    

#### Task 8: Verify the rules

1. List rules:
    
    ```bash
    sudo iptables -L -n -v
    ```
    
2. Expected lines (example):
    
    ```
    ACCEPT     tcp  --  172.16.238.14  0.0.0.0/0  tcp dpt:6200
    DROP       tcp  --  0.0.0.0/0       0.0.0.0/0  tcp dpt:6200
    ```
    

---

### Quick check

- **Expected result:** Only the LB can reach the app on port `6200`, and the rules remain after reboot.

---

### Optional: Connectivity test

- From the LB host (should succeed):
    
    ```bash
    curl http://<app-host-ip>:6200
    ```
    
- From another host (should fail/timeout):
    
    ```bash
    curl http://<app-host-ip>:6200
    ```
    

---

### Repeat for other ports (example: `3003`)

```bash
sudo iptables -A INPUT -p tcp -s 172.16.238.14 --dport 3003 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 3003 -j DROP
sudo iptables-save | sudo tee /etc/sysconfig/iptables
```

---

### Alternative: run a setup script on each app server

#### Task 1: Create the script

1. SSH into each app server.
2. Create a script file (example name `iptables-setup.sh`):
    
    ```bash
    sudo nano iptables-setup.sh
    ```
    
3. Paste the script below (edit `APP_PORT` and `LB_HOST` as needed):
    
    ```bash
    #!/bin/bash
    
    APP_PORT=6200   # change accordingly
    LB_HOST="stlb01"
    
    # Use full paths
    DNF=/usr/bin/dnf
    IPTABLES=/usr/sbin/iptables
    SYSTEMCTL=/usr/bin/systemctl
    GETENT=/usr/bin/getent
    AWK=/usr/bin/awk
    TEE=/usr/bin/tee
    IPTABLES_SAVE=/usr/sbin/iptables-save
    
    # Install iptables
    $DNF install -y iptables iptables-services
    
    # Enable and start iptables service
    $SYSTEMCTL enable iptables
    $SYSTEMCTL start iptables
    
    # Flush existing rules
    $IPTABLES -F
    
    # Get LB IP
    LB_IP=$($GETENT hosts $LB_HOST | $AWK '{print $1}')
    if [ -z "$LB_IP" ]; then
      echo "Error: Cannot resolve LB host IP"
      exit 1
    fi
    
    # Allow LB host to access the app port
    $IPTABLES -A INPUT -p tcp -s $LB_IP --dport $APP_PORT -j ACCEPT
    
    # Drop all other traffic to the app port
    $IPTABLES -A INPUT -p tcp --dport $APP_PORT -j DROP
    
    # Save rules for persistence
    $IPTABLES_SAVE | $TEE /etc/sysconfig/iptables
    
    echo "Iptables setup completed and rules are persistent after reboot."
    ```
    

#### Task 2: Make it executable and run it

1. Make executable:
    
    ```bash
    sudo chmod +x iptables-setup.sh
    ```
    
2. Run:
    
    ```bash
    sudo ./iptables-setup.sh
    ```