# 20. Advanced SSH

Aim of this task is to make ssh-server listen on non-standard port on top of commonly used - `22`. To ensure that servers are secured properly firewall service must be running as well as selinux mode set to `enforcing`

Create a playbook named `ssh.yml` that meets following requirements:
* Ensures that firewalld is installed and running on boot
* Opens 20022 in firewall for incoming connections
* Modifies sshd config to listen on both 22 and 20022
* Is executed against `webservers` group
* Uses system role selinux to enable enforcing mode and allow connection on port 20022
* Reboots machines as the last task that playbook executes
* Ensure that during playbook execution at least one server is available, configure it to run sequentially
Ensure that after reboot firewalld service is running, selinux mode set to `enforcing` and the machine can be accessed by both ports

You can use below command to verify the result
```bash
ssh -p 22 managed4.example.com exit && ssh -p 20022 -o StrictHostKeyChecking=no managed4.example.com exit
```
