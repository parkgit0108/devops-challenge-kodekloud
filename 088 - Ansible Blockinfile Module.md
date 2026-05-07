```sql
vi /home/thor/ansible/playbook.yml
```
```sql
---
- name: Configure httpd on app servers
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

    - name: Add content to index.html
      ansible.builtin.blockinfile:
        path: /var/www/html/index.html
        create: yes
        block: |
          Welcome to XfusionCorp!

          This is Nautilus sample file, created using Ansible!

          Please do not modify this file manually!

    - name: Set ownership on index.html
      ansible.builtin.file:
        path: /var/www/html/index.html
        owner: apache
        group: apache

    - name: Set permissions on index.html
      ansible.builtin.file:
        path: /var/www/html/index.html
        mode: '0777'
```
```sql
cd /home/thor/ansible
ansible-playbook -i inventory playbook.yml
```
