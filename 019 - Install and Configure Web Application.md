# Install and Configure Web Application

---

<aside>

**Purpose:** Install and configure Apache (httpd) to serve two sites (`/official` and `/demo`) on port **8086**, deploy the provided site backups, set permissions, and verify with `curl`.

</aside>

---

### Procedure

#### Task 1: Install Apache (httpd)

1. On **app server 3**, install Apache:
    
    ```bash
    sudo yum install -y httpd
    ```
    

#### Task 2: Configure Apache to listen on port 8086

1. Edit the Apache config:
    
    ```bash
    sudo vi /etc/httpd/conf/httpd.conf
    ```
    
2. Find:
    
    ```
    Listen 80
    ```
    
3. Change to:
    
    ```
    Listen 8086
    ```
    

#### Task 3: Start and enable Apache

1. Enable and start the service:
    
    ```bash
    sudo systemctl enable httpd
    sudo systemctl start httpd
    ```
    
2. Verify status:
    
    ```bash
    sudo systemctl status httpd
    ```
    

#### Task 4: Create directories for the websites

1. Create the required site directories:
    
    ```bash
    sudo mkdir -p /var/www/html/official
    sudo mkdir -p /var/www/html/demo
    ```
    

#### Task 5: Copy website backups from jump_host

1. From **jump_host**, copy backups to **app server 3**:
    
    ```bash
    scp -r /home/thor/official banner@stapp03:/tmp/
    scp -r /home/thor/demo banner@stapp03:/tmp/
    ```
    
2. On **app server 3**, copy content into the web root:
    
    ```bash
    sudo cp -r /tmp/official/* /var/www/html/official/
    sudo cp -r /tmp/demo/* /var/www/html/demo/
    ```
    

#### Task 6: Set correct permissions

1. Set ownership to Apache:
    
    ```bash
    sudo chown -R apache:apache /var/www/html/official
    sudo chown -R apache:apache /var/www/html/demo
    ```
    

#### Task 7: Restart Apache

1. Restart the service:
    
    ```bash
    sudo systemctl restart httpd
    ```
    

#### Task 8: Test

1. On **app server 3**, verify both paths respond:
    
    ```bash
    curl http://localhost:8086/official/
    curl http://localhost:8086/demo/
    ```
    

---

### Reference

```bash
sudo yum install -y httpd
sudo vi /etc/httpd/conf/httpd.conf
sudo systemctl enable httpd
sudo systemctl start httpd
sudo systemctl status httpd
sudo mkdir -p /var/www/html/official
sudo mkdir -p /var/www/html/demo
scp -r /home/thor/official banner@stapp03:/tmp/
scp -r /home/thor/demo banner@stapp03:/tmp/
sudo cp -r /tmp/official/* /var/www/html/official/
sudo cp -r /tmp/demo/* /var/www/html/demo/
sudo chown -R apache:apache /var/www/html/official
sudo chown -R apache:apache /var/www/html/demo
sudo systemctl restart httpd
curl http://localhost:8086/official/
curl http://localhost:8086/demo/
```