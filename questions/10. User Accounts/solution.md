# 10. User Accounts - Solution

The playbook might look as follows
```yml
---
- name: Setup accounts
  hosts: webservers
  become: true
  vars_files:
  - vars/users.yml
  - vars/regular_users.yml
  tasks:
  - name: Create users for webserver group
    user:
      name: "{{ item.username }}"
      state: present
      uid: "{{ item.uid }}"
      groups: ['wheel']
      password: "{{ user_password | password_hash('sha512') }}"
      shell: /bin/bash
    loop: "{{ users }}"
    when: item.uid > 3000 
  - name: Copy key
    authorized_key:
      key: "{{ lookup('file', '/home/automation/.ssh/id_rsa.pub') }}"
      user: "{{ item.username }}"
    loop: "{{ users }}"
    when: item.uid > 3000
- name: Setup accounts
  hosts: database
  become: true
  vars_files:
  - vars/users.yml
  - vars/regular_users.yml
  tasks:
  - name: Create users for database group
    user:
      name: "{{ item.username }}"
      state: present
      groups: ['wheel']
      shell: /bin/bash
      password: "{{ user_password | password_hash('sha512') }}"
      uid: "{{ item.uid }}"
    loop: "{{ users }}"
    when: item.uid < 3000 and item.uid >= 2000
  - name: Copy key
    authorized_key:
      key: "{{ lookup('file', '/home/automation/.ssh/id_rsa.pub') }}"
      user: "{{ item.username }}"
    loop: "{{ users }}"
    when: 2000 <= item.uid < 3000
...
```

Call the playbook like as it is presented below
```bash
ansible-playbook users.yml --vault-id user@./secrets/regular_users_password
```