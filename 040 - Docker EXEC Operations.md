# Docker EXEC Operations

---

<aside>

**Purpose:** Access a running container, install Apache2, configure it to listen on port 3000, start the service, and verify it is running.

</aside>

---

### Procedure

#### Task 1: Access the running container

1. Exec into the container:
    
    ```bash
    docker exec -it kkloud bash
    ```
    

#### Task 2: Update packages and install Apache2

1. Update package index:
    
    ```bash
    apt update
    ```
    
2. Install Apache2:
    
    ```bash
    apt install -y apache2
    ```
    

#### Task 3: Configure Apache to listen on port 3000

#### Step 1: Install an editor (if needed) and edit ports config

1. Install vim (optional):
    
    ```bash
    apt install -y vim
    ```
    
2. Edit ports config:
    
    ```bash
    vi /etc/apache2/ports.conf
    ```
    
3. Change:
    
    ```
    Listen 80
    ```
    
    To:
    
    ```
    Listen 3000
    ```
    

#### Step 2: Update the default virtual host

1. Edit the default site:
    
    ```bash
    vi /etc/apache2/sites-available/000-default.conf
    ```
    
2. Change:
    
    ```
    <VirtualHost *:80>
    ```
    
    To:
    
    ```
    <VirtualHost *:3000>
    ```
    

> ⚠️ Do NOT bind to a specific IP — using `*` ensures it listens on all interfaces.
> 

#### Task 4: Start Apache service

1. Start Apache:
    
    ```bash
    service apache2 start
    ```
    

#### Task 5: Verify Apache is running

1. Check Apache status:
    
    ```bash
    service apache2 status
    ```
    

---

### Reference

```bash
docker exec -it kkloud bash
apt update
apt install -y apache2
apt install -y vim
vi /etc/apache2/ports.conf
vi /etc/apache2/sites-available/000-default.conf
service apache2 start
service apache2 status
```