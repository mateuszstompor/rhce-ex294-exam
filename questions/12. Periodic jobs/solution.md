# 11. Periodic jobs - Solution

The playbook might look as follows
```yml
---
- hosts: proxy
  become: true
  tasks:
  - name: Schedule greetings
    at:
      unique: true
      count: 15
      units: minutes
      command: "echo 'Greatings from {{ ansible_facts.fqdn }}' > /var/log/greetings; chown automation:automation /var/log/greetings;"
  - name: Schedule periodic date dump
    cron:
      weekday: Mon-Fri
      state: present
      job: "date >> /var/log/time.log"
      minute: '*/60'
      user: root
      month: '*'
      name: Log time periodically
...
```