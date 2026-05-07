```sql
vi /home/thor/ansible/playbook.yml
```
```sql
---
- name: Configure ACLs on app server 1
  hosts: stapp01
  become: yes

  tasks:
    - name: Create blog.txt
      ansible.builtin.file:
        path: /opt/finance/blog.txt
        state: touch
        owner: root
        group: root

    - name: Set ACL for group tony
      ansible.posix.acl:
        path: /opt/finance/blog.txt
        entity: tony
        etype: group
        permissions: r
        state: present

- name: Configure ACLs on app server 2
  hosts: stapp02
  become: yes

  tasks:
    - name: Create story.txt
      ansible.builtin.file:
        path: /opt/finance/story.txt
        state: touch
        owner: root
        group: root

    - name: Set ACL for user steve
      ansible.posix.acl:
        path: /opt/finance/story.txt
        entity: steve
        etype: user
        permissions: rw
        state: present

- name: Configure ACLs on app server 3
  hosts: stapp03
  become: yes

  tasks:
    - name: Create media.txt
      ansible.builtin.file:
        path: /opt/finance/media.txt
        state: touch
        owner: root
        group: root

    - name: Set ACL for group banner
      ansible.posix.acl:
        path: /opt/finance/media.txt
        entity: banner
        etype: group
        permissions: rw
        state: present
```
```sql
cd /home/thor/ansible
ansible-playbook -i inventory playbook.yml
```

