# 20. Advanced SSH - Solution

Your playbook might look as follows
```yml
---
- hosts: webservers
  become: true
  serial: 1
  vars:
    selinux_state: enforcing
    selinux_ports:
    - { ports: '20022', proto: 'tcp', setype: 'ssh_port_t', state: 'present' }
  tasks:
  - name: Install firewalld
    yum: 
      name: firewalld
      state: present
  - name: Ensure that firewalld is running
    service:
      name: firewalld
      state: started
      enabled: true
  - name: Open non-standard port for the users in firewall
    firewalld:
      port: 20022/tcp
      state: enabled
      permanent: true
      immediate: true
  - name: Ensure that server listens on non-standard port
    lineinfile:
      line: Port 20022
      path: /etc/ssh/sshd_config
  - name: Ensure that server listens on standard port
    lineinfile:
      line: Port 22
      path: /etc/ssh/sshd_config
  roles:
  - role: rhel-system-roles.selinux
  post_tasks:
  - name: Reboot the systems
    reboot:
...
```

To run the playbook go to `/home/automation/plays` and execute
```bash
ansible-playbook ssh.yml
```
