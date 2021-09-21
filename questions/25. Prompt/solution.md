# 25. Prompt - Solution

The playbook might look as follows:
```yml
- hosts: all
  become: true
  gather_facts: false
  vars:
    group_name: networking
  vars_prompt:
  - name: username
    prompt: Provide name for the user
    private: false
  - name: password
    prompt: Provide password for the user
    private: true
    confirm: true
    encrypt: sha512_crypt
  tasks:
  - name: Create group
    group:
      name: "{{ group_name }}"
  - name: Add group to sudoers
    copy:
      content: "%{{ group_name }} ALL = NOPASSWD: /usr/bin/nmcli\n"
      dest: /etc/sudoers.d/networking
  - name: Create the user
    user:
      name: "{{ username }}"
      password: "{{ password }}"
      groups: "['{{ group_name }}']"
```