# 1. Ansible Installation and Configuration

* Install the ansible package on the control node
* Create `automation` user with `devops` password, the user should be allowed to execute any command
without providing password to the prompt
* Create an inventory at `/home/automation/plays/inventory` on the control node with following requirements:
    * managed1.example.com should be a member of the proxy host group
    * managed2.example.com should be a member of the webservers host group
    * managed3.example.com should be a member of the webservers and database host group
    * managed4.example.com should be a member of the database host group
* Create a config file at `/home/automation/plays/ansible.cfg` with following requirements:
    * priviledged escalation is disabled by default
    * ansible should manage 10 hosts at a single time
    * use previously defined inventory file by default
    * roles path should include `/home/automation/plays/roles`
