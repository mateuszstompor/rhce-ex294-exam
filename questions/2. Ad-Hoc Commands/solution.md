# 2. Ad-Hoc Commands - Solution
Here is how the script might look like
```bash
#!/usr/bin/bash

# Create the directory for ssh keys
ansible localhost -m file -a "state=directory path=/home/automation/.ssh"
# Generate the keypair
ansible localhost -m openssh_keypair -a "path=/home/automation/.ssh/id_rsa"
# Create the user, calling it with sudo will avoid host key checking
PASSWORD_HASH=$(openssl passwd -6 devops)
sudo ansible all -m user -a "state=present name=automation password=$PASSWORD_HASH" -u root
# Make the hosts known
for HOST in $(ansible all --list-hosts | sed '1d')
do
    KEY=`sudo ssh-keyscan -t rsa $HOST 2> /dev/null`
    ansible localhost -m known_hosts -a "key=\"$KEY\" name=$HOST path=/home/automation/.ssh/known_hosts"
done
# Share public key with rest of the nodes, inventory is taken from the previous exercise
sudo ansible all -m authorized_key -a "user=automation key={{ lookup('file', '/home/automation/.ssh/id_rsa.pub') }}"
# Allow passwordless sudo
sudo ansible all -m copy -a "content='automation ALL=(ALL) NOPASSWD:ALL' dest=/etc/sudoers.d/automation"
```
Place it at `/home/automation/plays/adhoc`, don't forget to make it executeable
```bash
chmod 755 /home/automation/plays/adhoc
```