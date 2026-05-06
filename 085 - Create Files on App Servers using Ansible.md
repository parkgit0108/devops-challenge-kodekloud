```sql
ssh thor@jump-host
mkdir -p ~/playbook
vi ~/playbook/inventory
```
```sql
[app]
app1 ansible_host=stapp01 ansible_user=tony ansible_password=Ir0nM@n file_owner=tony
app2 ansible_host=stapp02 ansible_user=steve ansible_password=Am3ric@ file_owner=steve
app3 ansible_host=stapp03 ansible_user=banner ansible_password=BigGr33n file_owner=banner
```
```sql
vi ~/playbook/playbook.yml
```
```sql
---
- name: Create file on app servers
  hosts: app
  become: yes

  tasks:
    - name: Create /opt/webdata.txt with correct permissions and ownership
      ansible.builtin.file:
        path: /opt/webdata.txt
        state: touch
        mode: '0655'
        owner: "{{ file_owner }}"
        group: "{{ file_owner }}"
```
```sql
#from ~/playbook
ansible-playbook -i inventory playbook.yml
```
