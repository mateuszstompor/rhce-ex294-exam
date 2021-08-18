# 3. Archiving - Solution

The playbook might look as follows:
```yml
---
- hosts: database
  remote_user: automation
  tasks:
  - name: Restore ownership 
    file:
      recurse: true
      path: /backup
      owner: automation
      group: automation
      state: directory
    become: true
  - name: Create directory for backups
    file:
      path: /backup/mysql
      state: directory
  - name: Create the file
    copy:
      content: "stephanie;max;john"    
      dest: /backup/mysql/users.csv
  - name: Create the archive
    archive:
      path: /backup/mysql/users.csv
      dest: /backup/mysql/users_archive.gz
      format: gz
...
```

To run it call
```bash
ansible-playbook archive.yml 
```