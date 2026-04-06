# SElinux Installation and Configuration

---

<aside>

**Purpose:** Install SELinux packages and disable SELinux by setting `SELINUX=disabled` in `/etc/selinux/config`.

</aside>

---

### Procedure

#### Task 1: Install SELinux packages

1. Install SELinux packages:
    
    ```
    sudo dnf install selinux-policy selinux-policy-targeted policycoreutils
    ```
    

#### Task 2: Update SELinux configuration

1. Open the SELinux config file:
    
    ```
    sudo nano /etc/selinux/config
    
    or vi, choice of your editor
    ```
    
2. Add or update the line to:
    
    ```
    SELINUX=disabled
    ```
    

### Quick check

- **Expected result:** `/etc/selinux/config` contains `SELINUX=disabled`.