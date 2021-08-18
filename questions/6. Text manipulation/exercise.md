# 6. Text Manipulation

* Create a playbook that customizes ssh configuration with following requirements:
    * Is placed at `/home/automation/plays/ssh_config.yml`
    * Is run against all servers
    * Disables X11 forwarding
    * Disables root login
    * Sets banner to `/etc/motd`
    * Sets maxminal number of auth tries to 3
