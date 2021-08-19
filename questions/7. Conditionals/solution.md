# 7. Conditionals - Solution

The playbook might look as follows:

```yml
---
- name: Manage kernel configuration
  hosts: all
  vars:
    minimal_memory: 1024
  gather_facts: true
  tasks:
  - name: Ensure that system meets requirements
    when: ansible_facts.memtotal_mb < minimal_memory
    fail:
      msg: Server has less than required {{ minimal_memory }}MB of RAM
  - name: Set kernel param
    become: true
    sysctl:
      name: vm.swappiness
      value: '10'
      state: present
      reload: true
...
```