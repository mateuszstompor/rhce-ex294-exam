# 18. Templating - Solution

The template might look as follows
```yml
127.0.0.1 localhost {{ ansible_hostname }} {{ ansible_fqdn }}
127.0.1.1 localhost 
{% for host in groups['all'] %}
{{ hostvars[host]['ansible_eth1']['ipv4']['address'] }} {{ hostvars[host]['ansible_hostname'] }} {{ hostvars[host]['ansible_fqdn'] }}
{% endfor %}
```

Playbook definition 
```yml
---
- name: Configure hosts file
  hosts: all
  become: true
  tasks:
  - name: Copy hosts file
    template:
      src: templates/hosts.j2
      dest: /etc/hosts
...
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook hosts.yml
```