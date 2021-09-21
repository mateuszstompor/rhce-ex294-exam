# 7. Conditionals - Solution

The playbook might look as follows:

```yml
---
- name: Configure sysctl parameters
  hosts: all
  vars:
    ram_mb: 1024
  tasks:
  - name: Ensure that server meets memory requirements
    fail:
      msg: Server should have at least {{ ram_mb }}MB of ram
    when: ansible_memtotal_mb < ram_mb
  - name: Configure swappiness
    become: true
    sysctl:
      name: vm.swappiness
      value: '10'
      sysctl_set: true
      reload: true
...
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook system_control.yml 
```
