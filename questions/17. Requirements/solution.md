# 17. Requirements - Solution

Create the file with following content
```yml
---
- name: git
  scm: git
  src: https://github.com/geerlingguy/ansible-role-git
  version: 3.0.0 
```

Go to `/home/automation/plays` and execute
```bash
ansible-galaxy role install -r requirements.yml -p roles
```