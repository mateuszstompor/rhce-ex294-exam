# 1. Ansible Installation and Configuration - Solution

### Installing the ansible
```bash
yum install -y ansible
```

### Configuring the user account
1. Create an account
```bash
useradd automation
```
2. Set password
```bash
echo devops | passwd --stdin automation
```
3. Allow access to privileged commands
```bash
echo "automation ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/automation
```
### Creating inventory
1. Create directory for the inventory
```bash
mkdir -p /home/automation/plays
```
2. Create the inventory with following contents
```ini
[proxy]
managed1.example.com

[webservers]
managed2.example.com
managed3.example.com

[database]
managed3.example.com
managed4.example.com
```
Save it to `/home/automation/plays/inventory`

### Create the config file with following content
```ini
[defaults]
inventory = ./inventory
forks = 10
roles_path = ~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/home/automation/plays/roles

[privilege_escalation]
become = false
```
Save it to `/home/automation/plays/ansible.cfg`

### General thoughts
Ensure that you have proper ownership, to restore it call
```
chown -R automation:automation /home/automation
```
