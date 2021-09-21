# 2. Ad-Hoc Commands - Solution
Here is how the script might look like
```bash
#!/usr/bin/bash

# Create the directory for ssh keys
ansible localhost -m file -a 'path=/home/automation/.ssh state=directory'
# Generate the keypair
ansible localhost -m openssh_keypair -a "path=/home/automation/.ssh/id_rsa owner=automation group=automation type=rsa"
# Create the user, calling it with sudo will avoid host key checking
sudo ansible all -m user -a "name=automation password={{ 'devops' | password_hash('sha512', 'salt')}}"
# Share public key with rest of the nodes, inventory is taken from the previous exercise
sudo ansible all -m authorized_key -a "key={{ lookup('file', '/home/automation/.ssh/id_rsa.pub') }} user=automation"
# Allow passwordless sudo
sudo ansible all -m copy -a 'content="automation ALL=(ALL) NOPASSWD:ALL" dest=/etc/sudoers.d/automation'
HOSTS=$(ansible all --list-hosts | sed '1d')
# Make the hosts known
for HOST in $HOSTS
do
  KEY=$(ssh-keyscan -t rsa $HOST 2>/dev/null)
  ansible localhost -m known_hosts -a "key='${KEY}' name=$HOST path=/home/automation/.ssh/known_hosts" -b
done
```
Place it at `/home/automation/plays/adhoc`, don't forget to make it executeable
```bash
chmod 755 /home/automation/plays/adhoc
```