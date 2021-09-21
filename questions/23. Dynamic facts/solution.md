# 23. Extending facts - Solution

The script might look as below

```bash
#!/usr/bin/bash
PATH=/usr/share
SIZE=$(/usr/bin/du $PATH -s 2>/dev/null | /usr/bin/awk '{print $1}')
echo {\"$PATH\": $SIZE}
```

Playbook itself may be implemented as follows

```yml
---
- hosts: all
  become: true
  gather_facts: false
  tasks:
  - name: Create directory for the facts
    file: 
      state: directory
      path: "{{ item }}"
      mode: 0755
      owner: root
      group: root
    loop:
    - /etc/ansible
    - /etc/ansible/facts.d
  - name: Copy dynamic facts file
    copy:
      src: files/usage.fact
      dest: /etc/ansible/facts.d/usage.fact
      mode: 0755
      owner: root
      group: root
...
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook dynamic_facts.yml
```