# Debugging MariaDB Issues

---

<aside>

**Purpose:** Troubleshoot and recover a MariaDB service that is failing to start (systemd), including fixing common data directory permission issues.

</aside>

---

### Procedure

#### Task 1: SSH into the database server

1. Connect to the database server:
    
    ```bash
    ssh <user>@<db-server>
    ```
    

#### Task 2: Check MariaDB service status

1. Check the service status:
    
    ```bash
    systemctl status mariadb
    ```
    
    Example output:
    
    ```bash
    [peter@stdb01 ~]$ systemctl status mariadb
    ○ mariadb.service - MariaDB 10.5 database server
         Loaded: loaded (/usr/lib/systemd/system/mariadb.service; disabled; preset: disabled)
         Active: inactive (dead)
           Docs: man:mariadbd(8)
                 https://mariadb.com/kb/en/library/systemd/
    ```
    

#### Task 3: Enable and attempt to start MariaDB

1. Enable MariaDB to start on boot:
    
    ```bash
    sudo systemctl enable mariadb
    ```
    
2. Start MariaDB:
    
    ```bash
    sudo systemctl start mariadb
    ```
    
3. If it fails, you may see an error like:
    
    `Job for mariadb.service failed because the control process exited with error code.
    See "systemctl status mariadb.service" and "journalctl -xeu mariadb.service" for details.`
    

#### Task 4: Inspect logs for the failure reason

1. Re-check detailed status:
    
    ```bash
    sudo systemctl status mariadb.service
    ```
    
2. Review the systemd journal for MariaDB:
    
    ```bash
    sudo journalctl -xeu mariadb.service
    ```
    
    Example:
    
    `Apr 07 01:31:51 stdb01 systemd[1]: mariadb.service: Failed with result 'exit-code'.
    Apr 07 01:31:51 stdb01 systemd[1]: Failed to start MariaDB 10.5 database server.`
    

#### Task 5: Verify (and fix) MariaDB data directory permissions

1. Check ownership under `/var/lib/`:
    
    ```bash
    ls -ld /var/lib/mysql
    ```
    
    Example:
    
    ```bash
    drwxr-xr-x 1 root     mysql    4096 Dec  2 15:22 mysql
    drwxrwx--- 3 nginx    root     4096 Feb 18 09:44 nginx
    drwx------ 4 postgres postgres 4096 Feb 18 09:44 pgsql
    ```
    
2. If `/var/lib/mysql` is not owned by `mysql:mysql`, fix it:
    
    ```bash
    sudo chown -R mysql:mysql /var/lib/mysql
    sudo chmod 700 /var/lib/mysql
    ```
    

#### Task 6: Start MariaDB and confirm it is running

1. Start MariaDB:
    
    ```bash
    sudo systemctl start mariadb
    ```
    
2. Confirm it is active:
    
    ```bash
    systemctl status mariadb
    ```
    
    Expected example:
    
    ```bash
    ● mariadb.service - MariaDB 10.5 database server
         Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: disabled)
         Active: active (running) since Tue 2026-04-07 01:38:06 UTC; 10s ago
           Docs: man:mariadbd(8)
                 https://mariadb.com/kb/en/library/systemd/
        Process: 58187 ExecStartPre=/usr/libexec/mariadb-check-socket (code=exited, status=0/...)
        Process: 58209 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir mariadb.service (code=...)
        Process: 58369 ExecStartPost=/usr/libexec/mariadb-check-upgrade (code=exited, status=...)
       Main PID: 58337 (mariadbd)
         Status: "Taking your SQL requests now..."
    ```
    

---

### Quick check

- **Expected result:** `mariadb` shows **Active: active (running)** and stays up after restart.