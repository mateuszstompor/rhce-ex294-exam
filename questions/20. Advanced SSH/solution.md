# 20. Advanced SSH - Solution

Your playbook might look as follows
```yml
---
- hosts: database
  become: true
  vars:
    selinux_state: enforcing
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
  - name: Ensure that server listens on non-standard port
    lineinfile:
      line: Port 20022
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