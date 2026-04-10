# Install and Configure DB Server

---

<aside>

**Purpose:** Install and configure MariaDB (install service, start/enable, secure, create database + user, grant privileges, and verify).

</aside>

---

### Procedure

#### Task 1: Install MariaDB Server

1. Install MariaDB:
    
    ```bash
    sudo yum install -y mariadb-server
    ```
    

#### Task 2: Start and enable MariaDB

1. Start and Enable MariaDB:
    
    ```bash
    sudo systemctl start mariadb
    sudo systemctl enable mariadb
    ```
    

#### Task 3: Login to MariaDB

1. Open the MariaDB shell:
    
    ```bash
    sudo mysql
    ```
    

#### Task 4: Create database and user

1. Create the database:
    
    ```sql
    CREATE DATABASE kodekloud_db8;
    ```
    
2. Create the user:
    
    ```sql
    CREATE USER 'kodekloud_gem'@'localhost' IDENTIFIED BY '8FmzjvFU6S';
    ```
    
3. Grant privileges:
    
    ```sql
    GRANT ALL PRIVILEGES ON kodekloud_db8.* TO 'kodekloud_gem'@'localhost';
    ```
    
4. Apply changes:
    
    ```sql
    FLUSH PRIVILEGES;
    ```
    

#### Task 5: Verify (optional)

1. List databases:
    
    ```sql
    SHOW DATABASES;
    ```
    
2. Verify user exists:
    
    ```sql
    SELECT User, Host FROM mysql.user;
    ```
    

---

### Reference

```bash
sudo yum install -y mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
sudo mysql
```

```sql
CREATE DATABASE kodekloud_db8;
CREATE USER 'kodekloud_gem'@'localhost' IDENTIFIED BY '8FmzjvFU6S';
GRANT ALL PRIVILEGES ON kodekloud_db8.* TO 'kodekloud_gem'@'localhost';
FLUSH PRIVILEGES;
SHOW DATABASES;
SELECT User, Host FROM mysql.user;
```