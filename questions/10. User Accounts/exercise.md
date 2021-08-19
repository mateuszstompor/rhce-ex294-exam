# 10. User Accounts

You have been given defintions of variables for the task
```yml
---
users:
- username: adam
  uid: 2000
- username: greg
  uid: 2001
- username: robby
  uid: 3001
- username: xenia
  uid: 3002
...
```

Store a file with the above content at `/home/automation/plays/vars/users.yml`

Create a playbook that meets following requirements:
* Is placed at `/home/automation/plays/users.yml`
* Creates users whose id starts with `2` on webservers host group. Password should be taken from the variable stored at `/home/automation/plays/vars/user_password.yml` (created in previous exercise)
* Creates users whose id starts with `3` on database host group. Password should be taken from the variable stored at `/home/automation/plays/vars/user_password.yml` (created in previous exercise)
* Users should be part of supplementary group `wheel`
* Users' shell should be set to `/bin/bash`
* Password should use SHA512 hash format
* Each user should have a SSH key uploaded - use the key from the first exercise
* After running the playbook users should be able to SSH into their servers without providing password to prompt
