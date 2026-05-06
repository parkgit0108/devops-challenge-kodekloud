```sql
ssh thor@jump-host
mkdir -p /home/thor/playbook && cd /home/thor/playbook
vi inventory
```
```sql
[app]
stapp01 ansible_host=stapp01 ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=stapp02 ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n
```
```sql
vi /home/thor/playbook/playbook.yml
```
```sql
---
- name: Install sqlite on app servers
  hosts: app
  become: yes

  tasks:
    - name: Install sqlite package
      ansible.builtin.yum:
        name: sqlite
        state: present
```
```sql
ansible-playbook -i inventory playbook.yml
```
