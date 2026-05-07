```sql
vi /home/thor/ansible/playbook.yml
```
```sql
---
- name: Configure httpd and deploy sample page
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

    - name: Create index.html with initial content
      ansible.builtin.copy:
        dest: /var/www/html/index.html
        content: |
          This is a Nautilus sample file, created using Ansible!
        owner: apache
        group: apache
        mode: '0744'

    - name: Add welcome line at top of file
      ansible.builtin.lineinfile:
        path: /var/www/html/index.html
        line: "Welcome to Nautilus Group!"
        insertbefore: BOF

    - name: Ensure correct ownership and permissions
      ansible.builtin.file:
        path: /var/www/html/index.html
        owner: apache
        group: apache
        mode: '0744'
```
```sql
cd /home/thor/ansible
ansible-playbook -i inventory playbook.yml
```
