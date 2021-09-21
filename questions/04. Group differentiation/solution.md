# 4. Group differentiation - Solution

1. Create directories for groups
```bash
mkdir -p /home/automation/plays/group_vars
mkdir -p /home/automation/plays/group_vars/{proxy,database,webservers}
```

2. Populate yml for `proxy` group
```bash
echo "motd: Welcome to HAProxy server" > /home/automation/plays/group_vars/proxy/motd.yml
```

3. Populate yml for `database` group
```bash
echo "motd: Welcome to MySQL database" > /home/automation/plays/group_vars/database/motd.yml
```

4. Populate yml for `webservers` group
```bash
echo "motd: Welcome to Apache server" > /home/automation/plays/group_vars/webservers/motd.yml
```

5. Finally, Create the playbook
```yml
---
- name: Setup motd
  hosts: all
  become: true
  gather_facts: false
  tasks:
  - name: Populate the file
    copy:
      content: "{{ motd }}"
      dest: /etc/motd
      owner: root
      group: root
      mode: 644
...
```
To run it go to `/home/automation/plays` and call 
```bash
ansible-playbook motd.yml
```