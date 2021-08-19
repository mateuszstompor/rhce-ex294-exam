# 8. YUM repositories - Solution

The playbook might look as follows:
```yml
---
- name: Deploy mysql server
  hosts: database
  become: true
  tasks:
  - name: Add definition of the repo
    yum_repository:
      enabled: true
      file: mysql
      description: MySQL 5.7 Community Server
      state: present
      baseurl: http://repo.mysql.com/yum/mysql-5.7-community/el/6/$basearch/ 
      name: mysql57-community
      gpgcheck: true
      gpgkey: https://repo.mysql.com/RPM-GPG-KEY-mysql
  - name: Install mysql server
    yum:
      name: mysql-server
      state: present
  - name: Start and enable the service
    service:
      name: mysqld
      state: started
      enabled: true 
...
```

To run it execute
```bash
ansible-playbook yum.yml 
```