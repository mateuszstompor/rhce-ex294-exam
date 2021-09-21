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

Install git if it's not present
```
yum install -y git
```

Rember that you can use [online documentation](https://galaxy.ansible.com/docs/using/installing.html?highlight=requirements) during the exam