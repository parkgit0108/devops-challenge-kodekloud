```sql
vi /home/thor/ansible/playbook.yml
```
```sql
---
- name: Install and configure httpd
  hosts: all
  become: yes

  tasks:
    - name: Install httpd package
      ansible.builtin.yum:
        name: httpd
        state: present

    - name: Start and enable httpd service
      ansible.builtin.service:
        name: httpd
        state: started
        enabled: yes
```
```sql
cd /home/thor/ansible
ansible-playbook -i inventory playbook.yml
```
