# 3. Archiving - Solution

The playbook might look as follows:
```yml
---
- name: Create directory for archives
  hosts: localhost
  gather_facts: false
  become: true
  tasks:
  - name: Create folder for the archives
    file:
      path: /backup
      owner: automation
      group: automation
      state: directory
      mode: 0755
- name: Archive config files
  hosts: all
  become: true
  tasks:
  - name: Create folder for the archive
    file:
      path: /backup
      owner: automation
      group: automation
      state: directory
      mode: 0755
  - name: Create the archive
    archive:
      dest: /backup/configuration.gz
      format: gz
      path: /etc
      owner: automation
      group: automation
      mode: 0660
  - name: Fetch the archive
    fetch:
      src: /backup/configuration.gz
      dest: /backup/{{ ansible_hostname }}-configuration.gz                                         
      owner: automation
      group: automation
      mode: 0660
...
```

To run it call
```bash
ansible-playbook archive.yml 
```