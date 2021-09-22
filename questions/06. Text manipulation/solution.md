# 6. Text Manipulation - Solution

The playbook might look as follows:

```yml
---
- name: Configure sshd
  hosts: all
  become: true
  vars:
    config_path: /etc/ssh/sshd_config
  tasks: 
  - name: Disallow X11 forwarding
    lineinfile:
      regexp: '^X11Forwarding.*'
      path: "{{ config_path }}"
      line: X11Forwarding no
    notify: Restart the service
  - name: Set max auth tries
    lineinfile:
      regexp: '^MaxAuthTries.*'
      line: MaxAuthTries 3
      path: "{{ config_path }}"
    notify: Restart the service
  handlers:
  - name: Restart the service
    service:
      name: sshd
      state: restarted
...
```

To run it execute
```bash
ansible-playbook ssh_config.yml 
```