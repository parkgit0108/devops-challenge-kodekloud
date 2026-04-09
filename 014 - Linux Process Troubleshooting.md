# Linux Process Troubleshooting

---

<aside>

**Purpose:** Troubleshoot a Linux service/process issue by checking service state, identifying port conflicts, killing the offending process, and verifying app reachability from the jump host.

</aside>

---

### Procedure

#### Task 1: SSH into the target app server

1. SSH into the server specified in the lab:
    
    ```bash
    ssh <user>@<app-server>
    ```
    

#### Task 2: Check the web service status (example: httpd)

1. Check `httpd` status:
    
    ```bash
    sudo systemctl status httpd.service
    ```
    
2. Identify errors (failed state, missing config, permission issues, etc.).

#### Task 3: Install troubleshooting utilities (net-tools)

1. Install `net-tools`:
    
    ```bash
    sudo dnf install -y net-tools
    ```
    

#### Task 4: Check which process is using the required port

1. Check listening ports and owning process:
    
    ```bash
    sudo netstat -tlnup
    ```
    
2. Confirm whether the lab’s required port is already in use by another service.
    - Example: a `sendemail` process is using port `3003`.

#### Task 5: Stop the conflicting process

1. Identify the PID from the netstat output.
2. Kill the process:
    
    ```bash
    sudo kill -9 <PID>
    ```
    

---

### Quick check

- From the **jump host**, verify each app server responds on the expected port (example: `3003`):
    
    ```bash
    curl http://stapp01:3003
    curl http://stapp02:3003
    curl http://stapp03:3003
    ```
    
- **Expected result:** all curls succeed (no connection refused / timeout).