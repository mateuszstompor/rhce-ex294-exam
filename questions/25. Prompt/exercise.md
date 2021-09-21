# 25. Prompt

You were asked to write a playbook that creates account for new employees. The idea is to execute the playbook each time a new person joins the company. To ease the boarding process your playbook should ask the user for his username and password while executing. All the people that are going to execute the playbook are suppossed to be part of networking team. From time to time they will need to interact with nmcli tool but despite that they shouldn't have access to privileged commands

To achieve that create a playbook named `prompt.yml` at `/home/automation/plays` that meets following requirements:
* Asks for username of a new user
* Runs against all hosts
* Asks for his password - ensure that it is hidden while the user is typing it. The user should type the password twice
* Creates networking group
* Allows the networking group to call `nmcli` tool with `sudo` without password. Ensure that nmcli is the ONLY tool that the group is allowed to execute with root privileges
* Assigns the user to `networking` supplementary group