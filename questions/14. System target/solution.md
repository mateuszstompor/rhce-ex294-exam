# 14. System target - Solution

```yml
---
- hosts: all
  become: true
  tasks:
  - name: Change default target
    file:
      state: link
      dest: /etc/systemd/system/default.target
      src: /usr/lib/systemd/system/multi-user.target
      force: true
...
```

In order to execute the playbook run 
```bash
ansible-playbook system_target.yml
```