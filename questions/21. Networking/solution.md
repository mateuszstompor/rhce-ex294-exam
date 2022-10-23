# 21. Networking - Solution

The playbook may be implemented as below:
```yml
---
- hosts: managed1.example.com,managed4.example.com
  become: true
  roles:
  - name: rhel-system-roles.network
...
```

To differentiate hosts config separte vars definition should be placed at `host_vars` directory

#### /home/automation/plays/host_vars/managed1.example.com/connections.yml 
```yml
network_connections:
- name: Internal
  type: ethernet
  interface_name: eth2
  ip:
    address:
    - 192.168.57.101/24
  state: up
```

#### /home/automation/plays/host_vars/managed4.example.com/connections.yml 
```yml
network_connections:
- name: Internal
  type: ethernet
  interface_name: eth2
  ip:
    address:
    - 192.168.57.102/24
  state: up
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook network.yml
```

Ensure that you have `rhel-system-roles` package installed