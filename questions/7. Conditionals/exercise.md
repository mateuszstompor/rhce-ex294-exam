# 7. Conditionals

* Create a playbook that meets following requirements:
    * Is placed at `/home/automation/plays/system_control.yml`
    * Runs against all hosts 
    * If a server has more than 1024MB of RAM, then use sysctl to set vm.swppiness to 10
    * If a server has less or equal to 1024MB of RAM exist with error message `Server has less than required 1024MB of RAM`
    * Configuration change should survive server reboots