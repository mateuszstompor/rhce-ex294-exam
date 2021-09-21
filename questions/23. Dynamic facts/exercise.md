# 23. Extending facts

1. Create a script which is going to be used as a dynamic fact and and store it at `/home/automation/plays/files`. The script should print out what is disk usage of `/usr/share` folder. Once present on a machine after running setup module against it you should be able to see result as below

```
"ansible_facts": {
    [...]
    "ansible_local": {
        "usage": {
            "/usr/share": 11488
        }
    }
    [...]
```

2. Create a playbook that deploys the script to all machines. Ensure that group and owner is set to root but let anyone execute the script. Store the playbook at `/home/automation/plays/dynamic_facts.yml`