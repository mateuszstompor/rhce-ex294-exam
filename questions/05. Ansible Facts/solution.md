# 5. Ansible Facts - Solution

The playbook might look as follows
```yml
---
- name: Configure custom facts
  hosts: proxy
  become: true
  gather_facts: false
  tasks:
  - name: Ensure directories hierarchy exists
    file:
      state: directory
      path: /etc/ansible/facts.d
  - name: Dump fact
    copy:
      content: "[application]\nname=haproxy\n"
      dest: /etc/ansible/facts.d/environment.fact
      mode: 0644
...
```
To run it execute
```bash
ansible-playbook ansible_facts.yml 
```

Call the command below to verify:
```bash
ansible proxy -m setup | grep ansible_local -A 3
```
