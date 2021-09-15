# 19. System roles - Solution

Install system roles first
```bash
yum install -y rhel-system-roles
```

The playbook might look as follows
```yml
---
- hosts: all
  become: true
  vars:
    timesync_ntp_servers:
    - hostname: 1.pl.pool.ntp.org
      iburst: true
      pool: true
    - hostname: 2.pl.pool.ntp.org
      iburst: true
      pool: true
  roles:
    - rhel-system-roles.timesync
  post_tasks:
  - name: Set the timezone
    timezone:
      name: UTC
...
```
To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook time.yml
```