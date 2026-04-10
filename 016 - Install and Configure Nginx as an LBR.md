# Install and Configure Nginx as an LBR

---

<aside>

**Purpose:** Install Nginx and configure it as a load balancer (upstream + reverse proxy) for the app servers.

</aside>

---

### Procedure

#### Task 1: Confirm Apache/httpd is running on each app server

1. Log in to each app server and check which port Apache/httpd is listening on:
    
    ```bash
    sudo ss -tlnup
    ```
    
2. Note the port (example: `6200`) — you’ll use it in the Nginx upstream config.

#### Task 2: Install Nginx on the LBR server

1. Install Nginx:
    
    ```bash
    sudo yum install nginx -y
    ```
    
2. Enable Nginx:
    
    ```bash
    sudo systemctl enable nginx
    ```
    
3. Start Nginx:
    
    ```bash
    sudo systemctl start nginx
    ```
    

#### Task 3: Configure Nginx load balancing (upstream + proxy)

1. Edit the Nginx config:
    
    ```bash
    sudo vi /etc/nginx/nginx.conf
    ```
    
2. Add the upstream block inside the `http` section (before the `server` block):
    
    ```
    upstream stapp {
        server stapp01:6200;
        server stapp02:6200;
        server stapp03:6200;
    }
    ```
    
3. In the `server` block (port `80`), configure the reverse proxy:
    
    ```
    location / {
        proxy_pass http://stapp;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
    ```
    

#### Task 4: Validate and restart Nginx

1. Validate config:
    
    ```bash
    sudo nginx -t
    ```
    
2. Restart Nginx:
    
    ```bash
    sudo systemctl restart nginx
    ```
    

---

### Quick check

- Confirm Nginx is listening on port `80`:
    
    ```bash
    sudo ss -tlnup | grep nginx
    ```
    
- Test from a client / jump host (expect an HTTP response):
    
    ```bash
    curl -I http://<lbr-hostname-or-ip>
    ```