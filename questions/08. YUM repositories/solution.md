# 8. YUM repositories - Solution

The playbook might look as follows:
```yml
- hosts: database
  become: true
  gather_facts: false
  tasks:
  - name: Import GPG key
    rpm_key:
      key: https://repo.mysql.com/RPM-GPG-KEY-mysql
  - name: Add definition of the repo
    yum_repository:
      baseurl: http://repo.mysql.com/yum/mysql-5.7-community/el/6/$basearch
      gpgcheck: true
      gpgkey: https://repo.mysql.com/RPM-GPG-KEY-mysql
      name: mysql57-community
      description: 'MySQL 5.7 Community Server'
      enabled: true
...
```

To run it execute
```bash
ansible-playbook yum.yml 
```

Idea of using `rpm_key` module is to import the key to the internal list kept by `rpm` tool
