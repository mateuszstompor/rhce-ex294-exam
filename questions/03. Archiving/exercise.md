# 3. Archiving

* Create a playbook that meets following requirements:
    * Populates file stored at `/backup/mysql/users.csv` with content `stephanie;max;john`
    * A gzip archive containing `/backup/mysql/users.csv` is stored at `/backup/mysql/users_archive.gz`
    * User `automation` should be owner of `/backup` and everything underneath 
    * Is placed at `/home/automation/plays/archive.yml`
    * Runs against `database` host group 
