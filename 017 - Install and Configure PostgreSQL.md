# Install and Configure PostgreSQL

---

<aside>

**Purpose:** Install and configure PostgreSQL (create lab user + database, grant privileges, and verify).

</aside>

---

### Procedure

#### Task 1: SSH into the database server

1. SSH into the database server.

#### Task 2: Switch to the `postgres` user and open `psql`

1. Switch to the `postgres` user (if required in your environment) and start `psql`:
    
    ```sql
    sudo -i -u postgres
    psql
    ```
    

#### Task 3: Create the lab user and database

1. Create the user:
    
    ```sql
    CREATE USER kodekloud_<Lab_provided> WITH PASSWORD 'Lab_provided';
    ```
    
2. Create the database:
    
    ```sql
    CREATE DATABASE kodekloud_<Lab_provdied>;
    ```
    
3. Grant privileges on the database to the user:
    
    ```sql
    GRANT ALL PRIVILEGES ON DATABASE kodekloud_<Lab_provdied> TO kodekloud_<Lab_provdied>;
    ```
    

#### Task 4: Verify

1. List roles/users:
    
    ```sql
    \du
    ```
    
2. List databases:
    
    ```sql
    \l
    ```
    

---

### Reference

```sql
sudo -i -u postgres
psql
CREATE USER kodekloud_gem WITH PASSWORD '*FHqwp!f';
CREATE DATABASE kodekloud_db2;
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db2 TO kodekloud_gem;
\du
\l
```

<img width="1235" height="1084" alt="image" src="https://github.com/user-attachments/assets/63702d9c-1b2f-4e3a-aeb6-41c9a3913ef3" />
