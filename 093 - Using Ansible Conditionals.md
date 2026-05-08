```sql
#Save this as:
#/home/thor/ansible/playbook.yml
---
- hosts: all
  become: yes
  gather_facts: yes

  tasks:

    - name: Copy blog.txt to App Server 1
      copy:
        src: /usr/src/security/blog.txt
        dest: /opt/security/blog.txt
        owner: tony
        group: tony
        mode: '0744'
      when: ansible_nodename == "stapp01"

    - name: Copy story.txt to App Server 2
      copy:
        src: /usr/src/security/story.txt
        dest: /opt/security/story.txt
        owner: steve
        group: steve
        mode: '0744'
      when: ansible_nodename == "stapp02"

    - name: Copy media.txt to App Server 3
      copy:
        src: /usr/src/security/media.txt
        dest: /opt/security/media.txt
        owner: banner
        group: banner
        mode: '0744'
      when: ansible_nodename == "stapp03"
```
```sql
#run
ansible-playbook -i inventory playbook.yml
```




