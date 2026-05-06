# Create Ansible Inventory for App Server Testing

### Step 1: SSH to jump host and go to playbook directory

```
ssh thor@jump_host
cd /home/thor/playbook
ls -l
```

---

### Step 2: Create inventory file

```
vi /home/thor/playbook/inventory
```

Paste:

```
stapp03 ansible_host=stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n
```

Save and exit:

- Press `Esc`
- Type `:wq` and press Enter

---

### Step 3: Verify inventory content

```
cat /home/thor/playbook/inventory
```

Expected:

```
stapp03 ansible_host=stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n
```

---

### Step 4: Test Ansible connectivity (ping)

```
ansible stapp03 -i inventory -m ping
```

Expected:

```
stapp03 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

---

### Step 5: Run the playbook (validation)

```
ansible-playbook -i inventory playbook.yml
```