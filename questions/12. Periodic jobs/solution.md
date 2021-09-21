# 12. Periodic jobs - Solution

The playbook might look as follows
```yml
---
- hosts: proxy
  name: Setup periodic jobs
  gather_facts: false
  become: true
  tasks:
  - name: Schedule vmstat execution
    at:
      command: '/usr/bin/vmstat 2>/dev/null 1>/var/log/vmstat.log; chown automation:automation /var/log/vmstat.log'
      count: 1
      units: minutes
      unique: true
  - name: Schedule hourly job
    cron:
      name: Dump plugged devices
      weekday: '1-5'
      minute: '0'
      hour: '*'
      day: '*'
      month: '*'
      job: "echo ----- $(date \"+%m/%d/%y %H:%M\") >> /var/log/devices.log;lsblk >> /var/log/devices.log;chown root:root /var/log/devices.log"
...
```

Go to `/home/automation/plays` and execute
```bash
ansible-playbook periodic_jobs.yml
```