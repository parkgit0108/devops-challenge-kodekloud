# Troubleshoot and Create Ansible Playbook

```
vi /home/thor/ansible/inventory
```

Use the **correct hostname (`stapp03`)**, not just an IP.

### Fix the inventory file vi /home/thor/ansible/inventory

```
[app_servers]
stapp03 ansible_host=stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

> Using `ansible_host=stapp03` ensures it uses the internal DNS/hosts mapping (this avoids the timeout issue you hit earlier).
> 

---

# 2. Create the playbook

```
vi /home/thor/ansible/playbook.yml
```

### Playbook content:

```
---
- name: Create file on App Server 3
  hosts: app_servers
  become: yes
  tasks:
    - name: Create empty file
      file:
        path: /tmp/file.txt
        state: touch
```

---

# 3. Run exactly as required

Make sure you're in the correct directory:

```
cd /home/thor/ansible
ansible-playbook-i inventory playbook.yml
```