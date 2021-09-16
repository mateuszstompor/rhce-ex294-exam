# 22. Extending facts - Solution

The playbook might look as follows:
```yml
---
- hosts: all
  tasks:
  - name: Gather package facts
    when: inventory_hostname in groups["database"]
    package_facts:
      manager: auto
  - name: Print out facts
    debug:
      var: hostvars[item]['ansible_facts']
    loop: "{{ groups['all'] }}"
...
```
