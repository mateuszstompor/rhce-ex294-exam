# 11. Software Packages - Solution

In order to differentiate groups from each other you may want to use `group_vars`.
Navigate to `/home/automation/plays` and create a directory that is going to keep definitions for all groups
```bash
mkdir -p group_vars/all
```
Do the same for the specific groups you are going to use
```bash
mkdir -p group_vars/{proxy,database}
```

You will need a definition that is going to be common to all hosts and overriden if needed. 
Here is how it might look like
```yml
common_packages: ['tmux']
specific_packages: []
```
To dump it call
```bash
printf "common_packages: ['tmux']\nspecific_packages: []\n" > group_vars/all/common.yml
```

Depending on the host group `specific_packages` need to be modified.
In case of `database` belonging hosts it should look like it is presented below
```yml
specific_packages: ['tcpdump', 'lsof']
```
Note that only a sinlge variable is overriden.
To dump it call
```bash
echo "specific_packages: ['tcpdump', 'lsof']" > group_vars/database/packages.yml
```
Do the same for the `proxy` group adjusting list of packages at the same time to meet the requirements
```bash
echo "specific_packages: ['mailx', 'lsof']" > group_vars/proxy/packages.yml
```
Finally, here is how the playbook might look like

```yml
---
- name: Setup Packages
  hosts: all
  become: true
  tasks:
  - name: Install common packages
    yum:
      state: present
      name: "{{ common_packages }}"
  - name: Install group specific packages
    yum:
      state: present
      name: "{{ specific_packages }}"
...
```

In order to execute the playbook run 
```bash
ansible-playbook software_packages.yml
```