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
  - name: Disallow root login
    lineinfile:
      regexp: '^PermitRootLogin.*'
      path: "{{ config_path }}"
      line: PermitRootLogin no
  - name: Disallow X11 forwarding
    lineinfile:
      regexp: '^X11Forwarding.*'
      path: "{{ config_path }}"
      line: X11Forwarding no
  - name: Set banner
    lineinfile:
      regexp: '^Banner.*'
      line: Banner /etc/motd
      path: "{{ config_path }}"
  - name: Set max auth tries
    lineinfile:
      regexp: '^MaxAuthTries.*'
      line: MaxAuthTries 3
      path: "{{ config_path }}" 
...
```