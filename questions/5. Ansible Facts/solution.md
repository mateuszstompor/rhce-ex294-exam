# 5. Ansible Facts - Solution

The playbook might look as follows
```yml
---
- name: Configure custom facts
  hosts: database
  become: true
  tasks:
  - name: Create facts directory
    file:
      state: directory
      mode: 0755
      path: /etc/ansible/facts.d
    become: true
  - name: Add custom fact
    copy:
      content: "[local]\nrole=mysql"
      dest: /etc/ansible/facts.d/database.fact
      mode: 0644
...
```
Call the command below to verify:
```bash
ansible database -m setup | grep ansible_local -A 3
```