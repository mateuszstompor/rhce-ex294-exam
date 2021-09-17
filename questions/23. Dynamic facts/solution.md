# 23. Extending facts - Solution

The script might look as below

```bash
#!/usr/bin/bash
PATH=/usr/share
USAGE=`/usr/bin/du $PATH -s | /usr/bin/awk '{print $1}'`
echo {\"$PATH\":\"$USAGE\"}
```

Playbook itself may be implemented as follows

```yml
---
- hosts: all
  become: true
  tasks:
  - name: Ensure that parent folder exists
    file:
      path: /etc/ansible
      mode: 0755
      owner: root
      group: root
      state: directory
  - name: Ensure that the folder exists
    file:
      path: /etc/ansible/facts.d
      state: directory
      owner: root
      group: root
      mode: 0755
  - name: Populate script to all hosts
    copy: 
      src: files/usage.fact
      dest: /etc/ansible/facts.d
      mode: 0755
      owner: root
      group: root
...
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook dynamic_facts.yml
```