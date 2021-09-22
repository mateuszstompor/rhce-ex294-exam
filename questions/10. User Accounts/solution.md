# 10. User Accounts - Solution

The playbook might look as follows
```yml
- hosts: all
  become: true
  gather_facts: false
  vars_files:
  - vars/users.yml
  - vars/regular_users.yml
  tasks:
  - name: Create users for webservers
    user:
      name: "{{ item.username }}"
      uid: "{{ item.uid }}"
      groups: ['wheel']
      shell: /usr/bin/bash
      password: "{{ user_password | password_hash('sha512', 'salt') }}"
    loop: "{{ users }}"
    when: |
      (item.uid >= 2000 and item.uid < 3000 and inventory_hostname in groups['webservers']) or
      (item.uid >= 3000 and item.uid < 4000 and inventory_hostname in groups['database'])
  - name: Upload key
    authorized_key:
      key: '{{ lookup("file", "/home/automation/.ssh/id_rsa.pub") }}'
      user: "{{ item.username }}"
    loop: "{{ users }}"
    when: |
      (item.uid >= 2000 and item.uid < 3000 and inventory_hostname in groups['webservers']) or
      (item.uid >= 3000 and item.uid < 4000 and inventory_hostname in groups['database'])
```

Call the playbook like as it is presented below
```bash
ansible-playbook users.yml --vault-id user@./secrets/regular_users_password
```
