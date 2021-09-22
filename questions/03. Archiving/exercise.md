# 3. Archiving

* Create a playbook that meets following requirements:
    * Creates a gzip archive containing `/etc` and stores it at `/backup/configuration.gz` on the managed hosts
    * Is placed at `/home/automation/plays/archive.yml`
    * Runs against `all` host group 
    * Retrieves archives from the managed nodes and stores them at `/backup/<hostname>-configuration.gz` on the control node
    * User `automation` should be owner of `/backup` and everything underneath. Both on the managed hosts and the control node. Only owner and members of his group should be able to read and manage files inside. Anyone should be allowed to list contents of `/backup`.
