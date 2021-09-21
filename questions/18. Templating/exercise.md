# 18. Templating

Create a new folder named `templates` at `/home/automation/plays` and prepare there a template that is going to be used later to generete hosts file for each node from the inventory. General idea is described by the below scratch
```
127.0.0.1 localhost <local_short_name> <local_fqdn>
127.0.1.1 localhost
<ip_address_host1> <short_name_host1> <fqdn_host1>
<ip_address_host2> <short_name_host2> <fqdn_host2>
[...]
```
Set the name to `hosts.j2`

Create a playbook named `hosts.yml` that meets following requirements:
* Is placed at `/home/automation/plays/roles`
* Runs against all hosts
* Uses templating to populate `hosts.j2` created before to all hosts from the inventory
* After playbook execution it should be possible to reach from any node to a different one using ip, short name or fqdn