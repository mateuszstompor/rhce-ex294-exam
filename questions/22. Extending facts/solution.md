# 22. Extending facts - Solution

The playbook might look as follows:
```yml
---
- hosts: all
  tasks:
  - name: Gather package facts
    when: inventory_hostname in groups["database"]
    package_facts:
  - name: Print out facts
    debug:
      var: ansible_facts
...
```
