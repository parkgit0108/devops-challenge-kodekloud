# Configure Nginx + PHP-FPM Using Unix Sock

---

<aside>

**Purpose:** Install Nginx and PHP-FPM, then configure Nginx to pass PHP requests to PHP-FPM via a Unix socket.

</aside>

---

### Procedure

#### Task 1: Connect to the app server

1. SSH into the app server (as specified in the lab).

#### Task 2: Install Nginx

1. Install Nginx:
    
    ```bash
    sudo dnf install nginx -y
    ```
    

#### Task 3: Configure Nginx to handle PHP via Unix socket

1. Edit the main Nginx config:
    
    ```bash
    sudo vi /etc/nginx/nginx.conf
    ```
    
2. Update the `server` block as needed (port differs per lab):
    
    ```jsx
    server {
        listen 8096; # port is different in each lab
        root /var/www/html;
        index index.php index.html;
    
        location ~ \.php$ {
            include fastcgi_params;
            fastcgi_pass unix:/var/run/php-fpm/default.sock;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    }
    ```
    

#### Task 4: Install PHP-FPM

1. Enable the required repositories (if needed by the lab image):
    
    ```bash
    sudo dnf install -y epel-release
    sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
    ```
    
2. Reset and enable the required PHP module stream (version differs per lab):
    
    ```bash
    sudo dnf module reset php -y
    sudo dnf module enable php:remi-8.3 -y # version is different in each lab
    ```
    
3. Install PHP and PHP-FPM:
    
    ```bash
    sudo dnf install -y php php-fpm
    ```
    

#### Task 5: Configure PHP-FPM to listen on a Unix socket

1. Create the runtime directory if not already:
    
    ```bash
    sudo mkdir -p /var/run/php-fpm
    ```
    
2. Edit the PHP-FPM pool config:
    
    ```bash
    sudo vi /etc/php-fpm.d/www.conf
    
    #Update the following settings:
    user = nginx
    group = nginx
    
    listen = /var/run/php-fpm/default.sock
    listen.owner = nginx
    listen.group = nginx
    listen.mode = 0660
    ```
    

#### Task 6: Enable and start services

1. Enable and start Nginx and PHP-FPM:
    
    ```bash
    sudo systemctl enable --now nginx
    sudo systemctl enable --now php-fpm
    ```
    

---

### Quick check

- Validate Nginx config:
    
    ```bash
    sudo nginx -t
    ```
    
- Confirm Nginx is listening on the expected port (e.g. `8096`):
    
    ```bash
    sudo ss -tlnup | grep nginx
    ```
    
- Confirm the PHP-FPM socket exists:
    
    ```bash
    sudo ls -l /var/run/php-fpm/default.sock
    ```
    
- Test from the jump host / client (as required by the lab):
    
    ```bash
    curl -I http://<app-hostname>:8096
    ```