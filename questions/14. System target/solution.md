# 14. System target - Solution

```yml
---
- hosts: all
  gather_facts: false
  become: true
  tasks:
  - name: Set the default target
    file:
      dest: /etc/systemd/system/default.target
      src: /usr/lib/systemd/system/multi-user.target
      state: link
...
```

In order to execute the playbook run 
```bash
ansible-playbook system_target.yml
```