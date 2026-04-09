# Setup SSL for Nginx

---

<aside>

**Purpose:** Install Nginx, configure SSL/TLS with the provided certificate + key, and verify HTTPS access (including HTTP → HTTPS redirect).

</aside>

---

### Procedure

#### Task 1: Install Nginx

1. Install Nginx:
    
    ```bash
    sudo dnf install nginx -y
    ```
    

#### Task 2: Enable and start the Nginx service

1. Enable Nginx:
    
    ```bash
    sudo systemctl enable nginx
    ```
    
2. Start Nginx:
    
    ```bash
    sudo systemctl start nginx
    ```
    
3. Check status:
    
    ```bash
    sudo systemctl status nginx
    ```
    

#### Task 3: Install certificate and key

1. Create the SSL directory:
    
    ```bash
    sudo mkdir -p /etc/nginx/ssl
    ```
    
2. Move the certificate and key into place:
    
    ```bash
    sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
    sudo mv /tmp/nautilus.key /etc/nginx/ssl/
    ```
    
3. Set permissions:
    
    ```bash
    sudo chmod 600 /etc/nginx/ssl/nautilus.key
    sudo chmod 644 /etc/nginx/ssl/nautilus.crt
    ```
    

#### Task 4: Update the Nginx configuration (HTTPS + redirect)

1. Edit the config:
    
    ```bash
    sudo vi /etc/nginx/nginx.conf
    ```
    
2. Add/update the server blocks (adjust `server_name` as needed):
    
    ```
    # SSL enabled Server
    server {
        listen 443 ssl;
        server_name 172.16.238.10;
    
        ssl_certificate     /etc/nginx/ssl/nautilus.crt;
        ssl_certificate_key /etc/nginx/ssl/nautilus.key;
    
        ssl_protocols       TLSv1.2 TLSv1.3;
        ssl_ciphers         HIGH:!aNULL:!MD5;
    
        root /usr/share/nginx/html;
        index index.html;
    
        location / {
            try_files $uri $uri/ =404;
        }
    }
    
    # Redirect HTTP to HTTPS
    server {
        listen 80;
        listen [::]:80;
        server_name 172.16.238.10;
    
        return 301 https://$host$request_uri;
    }
    ```
    

#### Task 5: Validate and reload Nginx

1. Validate config:
    
    ```bash
    sudo nginx -t
    ```
    
2. Reload Nginx:
    
    ```bash
    sudo systemctl reload nginx
    ```
    

#### Task 6: Add a quick test page

1. Write a simple index page:
    
    ```bash
    echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
    ```
    

---

### Quick check

- Test `curl` from the jump host (expect `200`):
    
    ```bash
    curl -k -I https://172.16.238.10
    ```
    
- Confirm HTTP redirects to HTTPS (expect `301` / `302`):
    
    ```bash
    curl -I http://172.16.238.10
    ```