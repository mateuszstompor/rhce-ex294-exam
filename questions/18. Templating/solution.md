18. Templating - Solution

The template might look as follows
```yml
127.0.0.1 localhost {{ ansible_facts.hostname }} {{ ansible_facts.fqdn  }}
{% for host in groups["all"] %}
{{ hostvars[host]['ansible_facts']['eth1']['ipv4']['address'] }} {{ hostvars[host]['ansible_facts']['hostname']  }} {{ hostvars[host]['ansible_facts']['fqdn'] }} 
{% endfor %}
```

Playbook definition 
```yml
- hosts: all
  become: true
  tasks:
  - name: Populate template with values
    template:
      src: hosts.j2
      dest: /etc/hosts
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook hosts.yml
```