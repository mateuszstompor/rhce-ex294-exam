# 2. Ad-Hoc Commands

* Write a script that meets following requirements:
    * Generates a SSH keypair
    * Is stored at `/home/automation/plays/adhoc`
    * Uses ansible ad-hoc commands
    * Creates `automation` user on all inventory hosts, `devops` is used as its password
    * Populates SSH key to all inventory hosts, access of `automation` user to any of them is allowed without password
    * `automation` user is allowed to escalate privileges on all inventory hosts without providing password

Ensure that the script works properly when `automation` user executes it 
