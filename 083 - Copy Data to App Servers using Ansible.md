```sql
ssh thor@jumphost
cd /home/thor/ansible
vi inventory
stapp01 ansible_user=tony ansible_ssh_password=Ir0nM@n
stapp02 ansible_user=steve ansible_ssh_password=Am3ric@
stapp03 ansible_user=banner ansible_ssh_password=BigGr33n
```
```sql
vi playbook.yml

---
- name: Deploy index.html to App Server 3
  hosts: app_servers
  become: yes

  tasks:
    - name: Ensure destination directory exists
      ansible.builtin.file:
        path: /opt/sysops
        state: directory
        owner: root
        group: root
        mode: '0755'

    - name: Copy index.html to App Server 3
      ansible.builtin.copy:
        src: /usr/src/sysops/index.html
        dest: /opt/sysops/index.html
        owner: root
        group: root
        mode: '0644'
```

```sql
ansible-playbook -i inventory playbook.yml
```
